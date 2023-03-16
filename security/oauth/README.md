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
Scopes are bundles of permissions coded into the application.

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
