# JWT
Securely transfer information using JSON.  The data is digitally signed so it is immutable after creation.  i.e. recipient can tell if it was modified in transit.
https://jwt.io/introduction

## Structure
3 parts separated by dots `.`
* Header
* Payload
* Signature

Format: `xxxxx.yyyyy.zzzzz`

Real JWT token example in HTTP request (OAuth2.0) (`Authorization: Bearer` header contains the JWT token, in OAuth2 this token is known as the `access_token`:
```HTTP
GET /calendar/v1/events
Host: api.example.com
    
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwczovL2V4YW1wbGUuYXV0aDAuY29tLyIsImF1ZCI6Imh0dHBzOi8vYXBpLmV4YW1wbGUuY29tL2NhbGFuZGFyL3YxLyIsInN1YiI6InVzcl8xMjMiLCJpYXQiOjE0NTg3ODU3OTYsImV4cCI6MTQ1ODg3MjE5Nn0.CA7eaHjIHz5NxeIJoFK9krqaeZrPLwmMmgI_XiQiIkQ
```

Decoding the JWT and checking the signature via command line:
JWT Token:
```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwczovL2V4YW1wbGUuYXV0aDAuY29tLyIsImF1ZCI6Imh0dHBzOi8vYXBpLmV4YW1wbGUuY29tL2NhbGFuZGFyL3YxLyIsInN1YiI6InVzcl8xMjMiLCJpYXQiOjE0NTg3ODU3OTYsImV4cCI6MTQ1ODg3MjE5Nn0.CA7eaHjIHz5NxeIJoFK9krqaeZrPLwmMmgI_XiQiIkQ
```

Bash script to decode and validate this token, note that you would need to client secret to check the signature:
```bash
base64url::encode () { base64 -w0 | tr '+/' '-_' | tr -d '='; }
base64url::decode () { awk '{ if (length($0) % 4 == 3) print $0"="; else if (length($0) % 4 == 2) print $0"=="; else print $0; }' | tr -- '-_' '+/' | base64 -d; }

echo -n 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9' \
| base64url::decode
{"alg":"HS256","typ":"JWT"}

echo -n 'eyJpc3MiOiJodHRwczovL2V4YW1wbGUuYXV0aDAuY29tLyIsImF1ZCI6Imh0dHBzOi8vYXBpLmV4YW1wbGUuY29tL2NhbGFuZGFyL3YxLyIsInN1YiI6InVzcl8xMjMiLCJpYXQiOjE0NTg3ODU3OTYsImV4cCI6MTQ1ODg3MjE5Nn0' \
| base64url::decode
{"iss":"https://example.auth0.com/","aud":"https://api.example.com/calandar/v1/","sub":"usr_123","iat":1458785796,"exp":1458872196}

CLIENT_SECRET=...
echo -n 'eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpc3MiOiJodHRwczovL2V4YW1wbGUuYXV0aDAuY29tLyIsImF1ZCI6Imh0dHBzOi8vYXBpLmV4YW1wbGUuY29tL2NhbGFuZGFyL3YxLyIsInN1YiI6InVzcl8xMjMiLCJpYXQiOjE0NTg3ODU3OTYsImV4cCI6MTQ1ODg3MjE5Nn0' \
| openssl dgst -sha256 -binary -hmac $CLIENT_SECRET | base64url::encode
```

### Header
Example header, this gets Base64Url encoded making the first part `xxxxx`
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### Payload
Contains the claims. Claims are statements about a user (or entity).

3 types of claims:
1. registered - predefined, not mandatory - iss (issuer), exp (expiration time), sub (subject), aud (audience), and [others](https://tools.ietf.org/html/rfc7519#section-4.1).
2. public - can be custom defined - to avoid name conflict, register with [IANA](https://www.iana.org/assignments/jwt/jwt.xhtml) or use fully qualified URI to properly namespace avoiding collision.
3. private - fully custom to share info between parties

Examle payload (also gets Base64Url encoded):
```json
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true
}
```

## Signature
To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.

For example, if we are using HMAC SHA256 the signature would be created like this:
```javascript
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```

## Final output

The output is three Base64-URL strings separated by dots that can be easily passed in HTML and HTTP environments, while being more compact when compared to XML-based standards such as SAML.

![image](https://user-images.githubusercontent.com/2372994/236962244-7fd541a1-21ed-4581-9ed1-25014878cacb.png)

Try JWT here: https://jwt.io/#debugger-io
