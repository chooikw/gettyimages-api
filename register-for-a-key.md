# Registering for an API key

### If you already have a Mashery Member account

1. <a href="https://developer.gettyimages.com/login/login" target="_blank">Sign in</a> with your Mashery Member credentials.
2. Click the **My Account** link near the top right of the page.
3. Click the **Get API keys** button.
4. Register your application and select your desired type of Api-Key. We provide two key options.
    -  **Issue a new key for Getty Test**
        - Use to test Getty Images API functionality including: image search and metadata, download, and account management.
    - **Issue a new key for Getty Images Embed**
        - Use to search for and embed from over 40 million embeddable images.

### If you do not have a Mashery Member account

1. <a href="https://developer.gettyimages.com/member/register" target="_blank">Register</a> a new Mashery Member account and your application.
2. Select your desired type of Api-Key. We provide two key options.
    -  **Issue a new key for Getty Test**
        - Use to test Getty Images API functionality including: image search and metadata, download, and account management.
    - **Issue a new key for Getty Images Embed**
        - Use to search for and embed from over 40 million embeddable images.
3. Click **Register**. You will receive an email presently with a confirmation link. Click the link.
4. Sign in with your Mashery Member credentials.

### After registering an application and receiving an Api-Key

1. Finish reading this overview.
2. Play with and learn more about the technical details using our interactive <a href="https://api.gettyimages.com/swagger/ui/index.html" target="_blank">documentation</a>.
3. Begin developing your application! All calls must be [authenticated](README.md#authentication) with your Api-Key. To [authorize](#authorization) access to protected resources (e.g. `https://api.gettyimages.com/v3/downloads/{id}`) get an access token using the [OAuth 2 client credentials flow](oauth2.md#client-credentials-flow).
