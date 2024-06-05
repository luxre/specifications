# Sign In With LRE®

## Overview

Follow these instructions to add a "Sign In With LRE®" button to your website that opens a window and lets users sign in with their LRE® username and password. 

Provide us with desired application name and a callback URL, and we'll supply you with a client ID and the necessary scopes. 

This guide will walk you through the steps to include the LREAuth authentication script on your page, initialize it, and handle authentication events.

## Prerequisites

- A callback URL for your application
- A client ID and scopes provided by us.

## Setup

1. **Include the LREAuth Script**

   Add the following script tag to your HTML:

   ```html
   <script src="https://auth.luxuryrealestate.com/api/v1/lre-auth.js"></script>
   ```

2. **Initialization**

   You can initialize the LREAuth script using either meta tags or a configuration object. See the Configration Details documentation below for more information.

   **Using Meta Tags:**

   Add the following meta tags to your HTML head:

   ```html
   <meta name="lre-auth-client-id" content="YOUR_CLIENT_ID">
   <meta name="lre-auth-scope" content="YOUR_SCOPES">
   <meta name="lre-auth-callback-uri" content="YOUR_CALLBACK_URI">
   <meta name="lre-auth-state" content="YOUR_STATE">
   ```

   **Using Configuration Object:**

   Alternatively, you can initialize the LREAuth script programmatically:

   ```html
   <script type="text/javascript">
       LREAuth.init({
           clientId: 'YOUR_CLIENT_ID',
           scope: 'YOUR_SCOPES',
           callbackUri: 'YOUR_CALLBACK_URI',
           state: 'YOUR_STATE',
           usePopup: true
       });
   </script>
   ```

3. **Add the Sign-In Button**

   Add a div element to the page body with the id "lre-auth-signin." The script will add a clickable button into the div that will trigger the LREAuth flow:

   ```html
   <div id="lre-auth-signin"></div>
   ```
## Configuration Details

**Client ID**

This is a unique identifier provided to you by LRE®. It identifies your application and allows us to recognize it.

**Scopes**

Scopes define the level of access requested by your application. They specify what data your application can access on behalf of the user. For example, name and email scopes allow access to the user's name and email address. Multiple scopes are separated with a space. Example `name email`

**Callback URI**

The callback URI is the URL to which the our auth provider will send the authorization code after the user has logged in and granted access. This URL must be on the same domain as the page with the sign-in button, and it must exist but doesn't need to have any specific content. You will briefly see this page in the popup window before it closes.

Example: If your application is hosted at https://example.com, your callback URL could be https://example.com/oauth/callback.

**State**

The state parameter is a random string you can generate and pass with the authentication request. It is returned to your application by the OAuth provider to prevent CSRF attacks and to ensure the response belongs to the request initiated by your application.


## Handling Events

### Authorization Events

Clicking the sign in button will open a popup window where the user will sign in. This will trigger an event.

1. **Success Event**

   Listen for the `LREAuthSignInOnSuccess` event to handle successful authentication. After successful authentication `LREAuth.getUserInfo();` can be called to get basic information (name, email) for the authenticated user:

   ```javascript
   document.addEventListener('LREAuthSignInOnSuccess', (event) => {
       console.log('Success:', event.detail.data);
       console.log(LREAuth.accessToken);

       // Fetch user info
       LREAuth.getUserInfo().then(userInfo => {
           console.log(userInfo.name);
           console.log(userInfo.email);
       }).catch(error => {
           console.error('Error fetching user info:', error);
       });

       // Optionally redirect after successful sign-in
       window.location.replace("https://mydomain.com/where-to-after-login");
   });
   ```

2. **Failure Event**

   Listen for the `LREAuthSignInOnFailure` event to handle authentication failures:

   ```javascript
   document.addEventListener('LREAuthSignInOnFailure', (event) => {
       console.error('Failure:', event.detail.error);
   });
   ```



## Methods

### `LREAuth.init(options)`

Initializes the LREAuth script with the provided options.

**Parameters:**

- `clientId`: Your client ID. Provided by us.
- `scope`: The scopes required for your application. 
- `callbackUri`: This is the callback url.
- `state`: An optional state parameter for security.

### `LREAuth.getUserInfo()`

Fetches the authenticated user's information using the access token. This should be called after authentication.

## Example

Here’s a complete example of the HTML structure:

```html
<!DOCTYPE html>
<html>
<head>
    <meta name="lre-auth-client-id" content="YOUR_CLIENT_ID">
    <meta name="lre-auth-scope" content="YOUR_SCOPES">
    <meta name="lre-auth-callback-uri" content="YOUR_CALLBACK_URI">
    <meta name="lre-auth-state" content="YOUR_STATE">
</head>
<body>
    <div id="lre-auth-signin"></div>
    <script src="https://auth.luxuryrealestate.com/api/v1/lre-auth.js"></script>
    <script>
        // This method will take precedence over the lre-auth meta tags.
        // Use either the init method or the metatags for configuration.
        LREAuth.init({
            clientId: 'YOUR_CLIENT_ID',
            scope: 'name email',
            callbackUri: 'YOUR_CALLBACK_URI',
            state: '12345'
        });

        // Event Listeners 
        document.addEventListener('LREAuthSignInOnSuccess', (event) => {
            console.log('Success:', event.detail.data);
            console.log('Access Token:', LREAuth.accessToken);

            // Fetch user info
            LREAuth.getUserInfo().then(userInfo => {
                console.log(userInfo.name);
                console.log(userInfo.email);
            }).catch(error => {
                  console.error('Error fetching user info:', error);
            });

            // Redirect after successful sign-in
            window.location.replace("https://mydomain.com/where-to-after-login");
        });

        document.addEventListener('LREAuthSignInOnFailure', (event) => {
            console.error('Failure:', event.detail.error);
        });
    </script>
</body>
</html>
```

This documentation provides all the necessary steps and examples for integrating LRE® authentication into your client application. If you have any questions or need further assistance, please [contact us](mailto:websupport@luxre.com).
