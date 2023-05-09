# JWT
Securely transfer information using JSON.  The data is digitally signed so it is immutable after creation.  i.e. recipient can tell if it was modified in transit.
https://jwt.io/introduction

## Structure
3 parts separated by dots `.`
* Header
* Payload
* Signature

e.g.
`xxxxx.yyyyy.zzzzz`

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
```
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
```
