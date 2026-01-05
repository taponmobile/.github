[BACK](./5_Tap_on_Mobile_backend_API.md)

## 5.1 ToM backend API OAuth2 authentication

The Oauth2 token endpoint provides access tokens which are used to authenticate and authorise requests to protected resources as described in the ToM API and subsequent sections.

To request an access token it is required to provide a valid client ID and client secret.

### 5.1.1 Request Parameters

The following parameters are used in the OAuth2 token endpoint (/oauth2/token).

|Parameter|Description|Type|Condition|
|---------|-----------|----|---------|
|grant_type|A string indicating which grant type is being used: client_credentials|String|Mandatory|
|scope|The scope of the access token, indicating the permissions that are granted to the client|String|Optional (depends on API)|
|client_id|A unique identifier for the client application, issued by the authorization server|String|Mandatory|
|client_secret|A secret string used to authenticate the client application with the authorization server|String|Mandatory|

### 5.1.2 Response Parameters

The response from the token endpoint will include a number of parameters:

|Parameter|Description|Type|Condition|
|---------|-----------|----|---------|
|access_token|A string containing the access token, which will be used for the terminal authentication endpoint|String|Mandatory|
|scope|The scope of the access token, indicating the permissions that are granted to the client|String|Optional (depends on API)|
|token_type|The type of access token. For example “Bearer”|String|Mandatory|
|expires_in|The number of seconds before the access token expires and a new one must be requested|Integer|Mandatory|

[NEXT](./5_2_Retrieving_and_managing_merchants_terminal_structure.md)