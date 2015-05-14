# Getty Images API Authentication Workflow
Getty Images API uses a number of OAuth2 implementations depending on the specific need of the request.

## Sections
1. [Supported Flows](#supported-authorization-flows)
1. [Additional Reading](#additional-reading)
1. [Postman Collections](#postman-collections)

## Supported Authorization Flows
1. [Resource Owner](#resource-owner-flow)
    * [Token Behavior](#resource-owner-token-expiration-revocation-and-refreshing)
1. [Client Credentials](#client-credentials-flow)
    * [Token Behavior](#client-credentials-token-behavior)
1. [Implicit Grant](OAuth2ImplicitGrantWorkflow.md)
    * [Token Behavior](OAuth2ImplicitGrantWorkflow.md#implicit-grant-token-behavior)

## Resource Owner Flow
#### Summary
The resource owner flow is only for Getty Images and Getty Images partner applications. This grant type is suitable for clients capable of obtaining the resource owner's credentials. It is also used to migrate existing clients using direct authentication schemes such as HTTP Basic or Digest authentication to OAuth by converting the stored credentials to an access token.

##### Request

    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'grant_type=password&client_id=exampleApiKey&client_secret=exampleSecret&username=someUsername&password=WithSomePassword' https://api.gettyimages.com/oauth2/token

##### Response

    {
      "access_token": "123456",
      "refresh_token": "83729034",
      "token_type": "Bearer",
      "expires_in": "1800"
    }

#### Resource Owner Token Expiration, Revocation, and Refreshing
##### Expiration
The resource owner flow grants a 30-minute access token. If the client application needs to access content for the user longer than 30 minutes, it can use the refresh token to get a new access token that will also be valid for 30 minutes. The refresh token is valid for one year and can be used as many times as needed within that one year to get a new access token. The refresh token cannot be used directly for API access.

##### Revocation
Refresh tokens can be revoked when the user changes their password.

##### Refresh
The refresh token is good for one year and can be used to retrieve another 30-minute access token by calling the token endpoint with a grant type of 'refresh_token'.
###### Example refresh request:

    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'grant_type=refresh_token&client_id=exampleApiKey&client_secret=exampleSecret&refresh_token=83729034' https://api.gettyimages.com/oauth2/token

## Client Credentials Flow
### Summary
Client Credentials flow is for client applications that will not have individual users. An application token is created and limits the client application to operations that do not need user credentials. A Sandbox application (for trial development and without a licensing agreement) can only use Client Credential flow.

#### Request
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d 'grant_type=client_credentials&client_id=exampleApiKey&client_secret=exampleSecret' https://api.gettyimages.com/oauth2/token

#### Response
    {
        "access_token": "123456",
        "token_type": "Bearer",
        "expires_in": "1800"
    }

Note: The access token is good for 30 minutes

#### Client Credentials Token Behavior
##### Expiration
The client credential flow grants a 30 minute access token.  Once the token has expired, a call for a new access token is required.

## Additional Reading
Please refer to these links for more technical details about OAuth itself

1. [Full OAuth RFC](http://tools.ietf.org/html/rfc6749)
1. [Resource Owner Password Credentials](https://tools.ietf.org/html/rfc6749#section-4.3)
1. [Client Credentials](https://tools.ietf.org/html/rfc6749#section-4.4)
1. [Implicit](https://tools.ietf.org/html/rfc6749#section-4.2)

## Postman Collections
[OAuth Collection](https://raw.githubusercontent.com/gettyimages/gettyimages-api-postman/master/OAuthCollection.json)
