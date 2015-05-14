## Implicit Grant Flow

#### Summary
Getty Images requires this flow for 3rd party client applications. In this flow, the user authorizes the application to access their protected resources using the Getty Images authorization server. Developers follow these steps to get an access token for their application:

1. Client application calls the Auth endpoint (e.g., https://api.gettyimages.com/oauth2/auth/) and passes in the following information:
  * API key / client ID
  * redirect uri that has been registered with the Getty Images API (parameters may be added that are not registered)
  * response type of "token"
  * state (optional)

2. Client application redirects to our sign-in page, whose location is provided in the response to step 1.

3. End user signs in with their Getty Images or Thinkstock credentials, and clicks Authorize.

4. The API verifies the client and user credentials and then redirects to the client application with a long-lived access token.

#####Example request:

        GET https://api.gettyimages.com/oauth2/auth/?response_type=token&client_id=s6BhdRkqt3&state=xyz&redirect_uri=https%3A%2F%2Fclient%2Eexample%2Ecom%2Fcb HTTP/1.1

#####Example response:

        HTTP/1.1 302 Found
        Location: https://client.example.com/cb#access_token=2YotnFZFEjr1zCsicMWpAA&state=xyz&token_type=bearer

#### Implicit Grant Token Behavior
##### Expiration
Some resources accept longer-lived access tokens, depending on the sensitivity of the resource. For instance, search functionality accepts long-lived tokens (i.e., one year), whereas download functionality is protected by a shorter access token lifetime (i.e., one week).

Once an access token is no longer valid (has expired) for a given resource, a new access token must be retrieved to access that resource. The Implicit Grant flow does not support access token refresh. New access tokens must be retrieved via the Implicit Grant flow.

###### Revocation
Access tokens can also be revoked when the user changes their password. Revoked tokens cannot be used for any API access. 
