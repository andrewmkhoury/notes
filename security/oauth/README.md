# OAuth
1. open standard for authorization
2. authorizes clients with access tokens rather than credentials
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

## Learn about Google's OAuth using curl
https://www.youtube.com/watch?v=hBC_tVJIx5w
https://www.daimto.com/how-to-get-a-google-access-token-with-curl/

<img src="https://user-images.githubusercontent.com/2372994/236962607-1392c556-67e5-4857-b947-56881aad5133.png" width="300">


Oauth 3 calls:
1. Consent - prompt user to allow access:
   1. example url for consent screen: `https://accounts.google.com/o/oauth2/v2/auth?client_id=XXXX.apps.googleusercontent.com&redirect_uri=urn:ietf:wg:oauth:2.0:oob&scope=https://www.googleapis.com/auth/userinfo.profile&response_type=code`
   2. In this case we have a special `redirect_uri` and `response_type=code` so we can manually copy the code to use curl for testing / learning. 
   3. Example consent screen \
      <img src="https://user-images.githubusercontent.com/2372994/236963176-26f11508-ab0b-42da-a2e2-da483a403765.png" width="300">
   4. Output of this is an "Authorization Code" which is only valid for a few minutes
2. Exchange the authorization code for for an OAuth access token using a post:
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

