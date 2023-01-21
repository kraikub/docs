# Connecting to Kraikub OAuth 2.0 Provider
OAuth 2.0 is an open standard for authorization that allows users to share their private resources (e.g. data, files) stored on one site with another site without having to share their credentials.

The authorization code grant type is used to obtain both access tokens and refresh tokens and is optimized for confidential clients.

### Authorization flow
The flow for the authorization code grant type is as follows:

1. The user is directed to the authorization endpoint on the OAuth 2.0 provider's website.
2. The user logs in and grants permission for the client application to access their data.
3. The OAuth 2.0 provider redirects the user back to the client application with an authorization code.
4. The client application sends a request to the token endpoint on the OAuth 2.0 provider's website, passing along the authorization code and other information (e.g. client ID and secret) in order to exchange the authorization code for an access token and a refresh token.
5. The OAuth 2.0 provider sends the access token and refresh token back to the client application.
6. The client application can now use the access token to access the user's protected resources on the OAuth 2.0 provider's website.
7. To authorize an user's account on an OAuth 2.0 provider with the authorization code grant type, the client application must first redirect the user to the authorization endpoint on the OAuth 2.0 provider's website. The URL for this endpoint will typically be provided by the OAuth 2.0 provider in their documentation.

The client application must include the following parameters in the URL:

- response_type=code
- client_id={client_id} (replace {client_id} with the client ID provided by the OAuth 2.0 provider)
- redirect_uri={redirect_uri} (replace {redirect_uri} with the URL that the OAuth 2.0 provider should redirect the user to after they have granted permission)
- scope={scope} (replace {scope} with the scope of the resources the client application is requesting access to)
- state={state} (replace {state} with an optional value that will be included in the redirect URI and can be used to maintain state between the request and the callback)

Once user grants the permission the oauth2 provider will redirect the user to the provided redirect_uri along with the authorization code. Then client application will use this authorization code to get the access token and refresh token by sending a POST request to the token endpoint of the OAuth 2.0 provider, along with the following parameters in the request body:

- grant_type=authorization_code
- code={code} (replace {code} with the authorization code received from the authorization endpoint)
- redirect_uri={redirect_uri} (replace {redirect_uri} with the redirect URI provided in the initial request)
- client_id={client_id} (replace {client_id} with the client ID provided by the OAuth 2.0 provider)
- client_secret={client_secret} (replace {client_secret} with the client secret provided by the OAuth 2.0 provider)
The OAuth 2.0 provider will then return an access token and a refresh token in the response.
