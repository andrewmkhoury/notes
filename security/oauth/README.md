# OAuth
1. open standard for authorization
2. authorizes clients with access tokens rather than credentials (Bearer token is the same as "access token")
3. OAuth 2.0 is widely used (1.0 and 2.0 or different and not backwards compatible)
4. user sends an API key ID and secret (instead of user id and password)

## Flow
End User => Identity Provider creates signed token => End User sends token => web app or API

1. App requests authorization from User
2. User authorizes App and delivers proof
3. App presents proof of authorization to server to get a Token
4. Token is restricted to only access what the User authorized for the specific App

## Oauth Components:
* Scopes and Consent
* Actors
* Clients
* Tokens
* Authorization Server
* Flows

## Scopes
Scopes are bundles of permissions coded into the application.  They define level of authorization that your application needs to request of the user.

## Actors
* Resource Owner: User who owns the data.
* Resource Server: The API which stores data.
* Client: The application that wants to access your data.
* Authorization Server: The main engine of OAuth

## Oauth Tokens
https://www.oauth.com/oauth2-servers/access-tokens/
* String used to make authorized requests to make API requests as a user (Resource Owner).
* They must be kept confidential in transfer and storage.
* Token endpoint is a url where users request tokens for a user.

## Implicit Grant vs. Authorization Code Grant
**Auth Code Grant**
First retrieve an auth code after user consent.
1. User Login + Consent - response is an Authorization Code
2. Exchange code for an Access Token and Refresh token
3. Use the Access Token in HTTP header to access the API `Authorization: Bearer {access_token}`
4. When the access token expires then use the refresh token to refresh the access token

**Implicit Grant**
Skips auth code and goes directly to getting the access token.  No refresh token so user would consent each time.
1. Request the access token directly, user consents immediately - `response_type=token` -> `https://am.example.com:8443/am/oauth2/authorize?response_type=token&client_id=myClientID&redirect_uri=https://example.com/oauth`
2. Use token for API calls via HTTP header `Authorization: Bearer {access_token}`

## OAuth Guide
https://stackoverflow.blog/2022/12/22/the-complete-guide-to-protecting-your-apis-with-oauth2/

## Learn about Google's OAuth using curl
https://www.youtube.com/watch?v=hBC_tVJIx5w
https://www.daimto.com/how-to-get-a-google-access-token-with-curl/

<img src="https://user-images.githubusercontent.com/2372994/236962607-1392c556-67e5-4857-b947-56881aad5133.png" width="300">

Oauth 4 calls:
1. User Login + Consent - response is an Authorization Code
2. Exchange code for an Access Token and Refresh token
3. Use the Access Token in HTTP header to access the API `Authorization: Bearer {access_token}`
4. When the access token expires then use the refresh token to refresh the access token

### 1. Consent - prompt user to allow access:
   1. example url for consent screen: `https://accounts.google.com/o/oauth2/v2/auth?client_id=XXXX.apps.googleusercontent.com&redirect_uri=urn:ietf:wg:oauth:2.0:oob&scope=https://www.googleapis.com/auth/userinfo.profile&response_type=code`
   2. In this case we have a special `redirect_uri` and `response_type=code` so we can manually copy the code to use curl for testing / learning. 
   3. Example consent screen \
      <img src="https://user-images.githubusercontent.com/2372994/236963176-26f11508-ab0b-42da-a2e2-da483a403765.png" width="300">
   4. Output of this is an "Authorization Code" which is only valid for a few minutes
### 2. Exchange the authorization code for for an access token
   1. We send a POST to the token endpoint including our `client_id` and `client_secret`.  This part must be secure, the `client_secret` must be kept secret!  The `client_id` and `client_secret` are two things we were given when setting up oauth with google. 
   2. Curl command to get access code using authorization code (`grant_type` is `authorization_code` because that is what we are using to exchange for an access token and refresh token).
      ```bash
      curl -s \
      --request POST \
      --data "code=4/1AY0e-g7BhBt0QU9f5HTgNDGNR1GYtH12q4xvgL_D2Q34A&client_id=XXXX.apps.googleusercontent.com&client_secret=zYAoXDam3mqsdwabh3dQ3NTh&redirect_uri=urn:ietf:wg:oauth:2.0:oob&grant_type=authorization_code" \
      https://accounts.google.com/o/oauth2/token
      ```
   3. In response we get an `access_token` (only valid for 1hr), refresh token can be used to refresh the access token.
      ```json
      {
        "access_token": "ya29.a0AfH6SMDypscIeiyNnPRvoizz3NvvA6SZdk9U4K8h4MyQRRm29kEc2shdrskPZp71Q1roy8RqIm_7spufW84ozUoSTk0QKkQ",
        "expires_in": 3599,
        "refresh_token": "1//09Y5LQ0XRxjt-CgYIARAAGAkSNwF-L9IrYzyMnbGtJHgh-FTf6z79cBhQ1hsPUAk71HFgFwqyXoiwpIa-4eA",
        "scope": "https://www.googleapis.com/auth/userinfo.profile",
        "token_type": "Bearer"
      }
      ```
      Bearer token means that the "Bearer" of the token has access - no further authorization required with a Bearer token.  They are considered secure because they are only valid for a limited time - e.g. 1 hr.
### 3. Call the API
   1. Now, we can use the access token to call the API
   2. Use HTTP header `Authorization: Bearer ya29.a0AfH6SMDypscIeiyNnPRvoizz3NvvA6SZdk9U4K8h4MyQRRm29kEc2shdrskPZp71Q1roy8RqIm_7spufW84ozUoSTk0QKkQ`
### 4. Use refresh token to refresh access token
   1. Once the access token expires, we use the refresh token to refresh the access token:
   2. Curl example:
      ```
      curl -s \
      --request POST \
      --data 'client_id=XXXXX.apps.googleusercontent.com&client_secret=AoXDam3mqsdwabh3dQ3NTh&refresh_token=1//09PsxSjPF2dMnCgYIARAAGAkSNwF-L9IrnCeO3BOLt0d8MGTpDX-bIAP3zb-Jp9sZtACxtJuIromiYeCH_twCyJoiqRsE8R_zOdg&grant_type=refresh_token' \
      https://accounts.google.com/o/oauth2/token
      ```
   2. Note that `grant_type=refresh_token`
   3. Example response:
      ```
      {
        "access_token": "ya29.a0AfH6SMA_vRaZekKJnvylcviCdEF1mzkPUd2i5k5qhFpclvi7deVMAL1nE4Ci6S3e3z5L0hnhhgYW6KknQEXu3StsdzykuNG6Zd5J80wORd4",
        "expires_in": 3599,
        "scope": "https://www.googleapis.com/auth/userinfo.profile",
        "token_type": "Bearer"
      }
      ```

### Get user profile info
#### OpenID Connect
https://developers.google.com/identity/openid-connect/openid-connect


#### Google specific people api
Request for google profile info:
```
curl -H 'Accept: application/json' -H "Authorization: Bearer ya29.a0AfH6SMDe0-ToZWsfUpgPYw2BxHMIU8yRgW3-RiV0yBTjOZJZzOQVp3os3Kh2weJ50AHS_3oPvullLs_wfonlBMo37KabiO7-VJ6G3XbJQ37_ABpikL-tpMrlou3koA67lAiMY3exFY70zT5v7idlT8FDift1kg" \
https://people.googleapis.com/v1/people/me?personFields=names
```
Example response:
```
{
  "resourceName": "people/117200475532",
  "etag": "%EgUBAj03LhoEAQIFByIMR3BzQkR2c9",
  "names": [
    {
      "metadata": {
        "primary": true,
        "source": {
          "type": "PROFILE",
          "id": "11720047"
        }
      },
      "displayName": "Linda Lawton",
      "familyName": "Lawton",
      "givenName": "Linda",
      "displayNameLastFirst": "Lawton, Linda",
      "unstructuredName": "Linda Lawton"
    },
    {
      "metadata": {
        "source": {
          "type": "CONTACT",
          "id": "3faa96eb0"
        }
      },
      "displayName": "Linda Lawton",
      "familyName": "Lawton",
      "givenName": "Linda",
      "displayNameLastFirst": "Lawton, Linda",
      "unstructuredName": "Linda Lawton"
    }
  ]
}
```
