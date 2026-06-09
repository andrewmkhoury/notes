# macOS Network Troubleshooting

## Symptom: Random TCP connections hang / partial page loads

Some web pages load fine, others load partially and hang. Simple requests succeed but complex ones stall. Rebooting the OS fixes it temporarily.

DNS cache flush (`sudo dscacheutil -flushcache`) does **not** help because DNS itself is working — it's the TCP connections that stall after lookup.

## Common Causes & Fixes

### 1. Limit IP Address Tracking (most common)

macOS routes some traffic through Apple relay/proxy servers. When those proxies are degraded, TCP connections hang mid-stream non-deterministically.

**Fix**: Disable per network:
- System Settings → Wi-Fi → your network → Details → uncheck **Limit IP Address Tracking**
- Repeat for any other saved networks

### 2. iCloud Private Relay

Similar to above but applies globally across all networks if you have iCloud+.

**Fix**: System Settings → Apple ID → iCloud → **Private Relay** → turn off

### 3. Routing table bloat (VPN)

VPNs like GlobalProtect inject many static routes. Over long sessions this can cause the network stack to slow down.

**Check**:
```bash
netstat -rn | wc -l   # high numbers (200+) indicate route bloat
```

**Fix**: Disconnect/reconnect VPN, or restart the VPN service without a full reboot:
```bash
# GlobalProtect
sudo launchctl kickstart -k system/com.paloaltonetworks.gp
```

### 4. Socket / port exhaustion

**Check**:
```bash
# Count TCP states — many TIME_WAIT or FIN_WAIT entries indicate exhaustion
netstat -an | awk '{print $6}' | sort | uniq -c | sort -rn

# Check current socket count vs limits
sysctl net.inet.tcp.pcbcount net.inet.tcp.tw_pcbcount
```

**Fix**: Reduce `TIME_WAIT` lingering:
```bash
sudo sysctl -w net.inet.tcp.msl=1000   # default 15000ms
```
This is reset on reboot. To persist, add to `/etc/sysctl.conf`.

## Quick Diagnostic Commands

```bash
# Overall TCP state summary
netstat -an | awk '{print $6}' | sort | uniq -c | sort -rn

# Routing table size
netstat -rn | wc -l

# DNS resolution time (check if DNS is actually the problem)
time nslookup google.com

# Test connection to a known host
curl -v --max-time 10 https://google.com
```

## Nuclear Option (without full reboot)

Restart the entire network stack:
```bash
sudo ifconfig en0 down && sudo ifconfig en0 up
```
Or via GUI: System Settings → Network → turn Wi-Fi off/on.
