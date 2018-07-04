# sky-api-addin
[![npm](https://img.shields.io/npm/v/@blackbaud/sky-api-addin.svg)](https://www.npmjs.com/package/@blackbaud/sky-api-addin)
[![status](https://travis-ci.org/blackbaud/sky-api-addin.svg?branch=master)](https://travis-ci.org/blackbaud/sky-api-addin)

The SKY API add-in library facilitates creating custom add-ins to extend UI experiences within Blackbaud applications. There are various flavors of extension points, but the general pattern is the same. The add-in is registered by providing the URL that will be loaded in an iframe within the application.

This library must be used in your add-in for it to render in the Blackbaud application. The `AddinClient` class will integrate with the host page, passing data and commands between the host and the add-in.

## Installation

### Prerequisites
This library makes extensive use of [ES6-style Promises](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise), so in order to support browsers that do not yet have native support for Promises (such as Internet Explorer 11) you will need to include a Promise polyfill such as [`es6-promise`](https://github.com/stefanpenner/es6-promise) and use the [auto-polyfill feature](https://github.com/stefanpenner/es6-promise#auto-polyfill) of the library so that `Promise` is added to the global environment.  This will need to be loaded on your page before the add-in library.

### ES6/TypeScript
- Ensure that you have Node v6+ and NPM v3+. To verify this, run `node -v` and `npm -v` at the command line.
- Install the library as a dependency of your project by running `npm install @blackbaud/sky-api-addin --save` in your project's folder.

### Vanilla JavaScript/ES5
The SKY API add-in library is also distributed as a UMD bundle.  If you're using ES5 with Node or a tool like Browserify you can `require()` it:

```js
var BBSkyApiAddin = require('@blackbaud/sky-api-addin');
var client = new BBSkyApiAddin.AddinClient({...});
```

If you are not using a module loader at all, then you can load the `dist/bundles/sky-api-addin.umd.js` file onto your page via a `<script>` element or concatenated with the rest of your page's JavaScript, and access it via the global `BBSkyApiAddin` variable:

```js
// BBSkyApiAddin is global here.
var client = new BBSkyApiAddin.AddinClient({...});
```

## Usage

#### Initializing the add-in
All add-ins must use this library in order to show in the host application. You will need to construct the `AddinClient` and register for any callbacks from the host page that you wish to handle.  You *must* register for `init`, which will pass key context information to your add-in.

Your `init` function will be called with an arguments object that contains:

 - `envId` - The environment ID for the host page
 - `context` - Additional context of the host page, which will vary for different extension points.
 - `ready` - A callback to inform the add-in client that the add-in is initialized and ready to be shown.

Using the information provided in the `init` arguments, the add-in should determine if and how it should be rendered.  Then it should call the `ready` callback, informing the host page.

```js
var client = new AddinClient({
  callbacks: {
    init: (args) => {
      args.ready({ showUI: true, title: 'My Custom Tile Title' });
    }
  }
});
```
#### Tile and tab add-ins
For tile or tab add-ins, the URL for the add-in will be rendered in a visible iframe on the page, where you can render any custom content.  The iframe will initially be hidden until an initialize protocol is completed between the host and the add-in.

The host page will handle rendering the tile or tab component around the add-in iframe.  When calling the `ready` callback, the `title` field will indicate the title for the tile or tab component.  Initially, the entire tile/tab will be hidden, and will show on the page if `showUI` is set to `true` in the callback.  You can set it to `false` to indicate that the tile/tab should not be shown, based on the user's privileges or context of the current record, etc.

Tile and tab add-ins will automatically track the height of the add-in's content and resize its container accordingly.

<strong>Note</strong>:  at this time, only Tile add-ins are supported.  Tab add-ins are planned as a future enhancement.

#### Button add-ins (also not yet supported, but coming soon)
For button add-ins, the add-in iframe will always be hidden.  The `init` protocol is still used, where `showUI` indicates whether the button should show or not on the page.  The `title` field will specify the label for the button.

When doing a button add-in, an additional callback for `buttonClick` should be configured.  This will be invoked whenever the user clicks the button for the add-in to take action.

```js
var client = new AddinClient({
  callbacks: {
    init: (args) => {
      args.ready({ showUI: true, title: 'My Custom Button Label' });
    },
    buttonClick: () => {
      // Show a modal or take action.
    }
  }
});
```


#### Showing a modal
Add-ins are capable of launching a "modal" user experience to show more details or gather additional input from the user.  The modal will be rendered in a separate full-screen iframe to maximum the available real estate (meaning, it will not be scoped to the bounds of the add-in's iframe).

To launch a modal, call the `showModal` function on the client, passing the URL for the modal and any context data needed by the modal:

```js
// Parent add-in launching a modal
var client = new AddinClient({...});
client.showModal({
  url: '<modal-addin-url>',
  context: { /* arbitrary context object to pass to modal */ }
});
```
##### Modal add-in
The host page will launch a full screen iframe for the URL provided, and load it as an add-in the same way it does for other types of add-ins.  The modal page must also pull in the SKY API add-in library and make use of the `AddinClient`.

The modal add-in will be responsible for rendering the modal element itself (including any chrome around the modal content).  To create a native modal experience, the add-in may set the body background to `transparent` and launch a SKY UX modal within its full screen iframe.

As with a typical add-in, the modal add-in should register for the `init` callback and will receive `envId` in the arguments. The `context` field for arguments will match the context object passed into the `showModal` call from the parent add-in.  Note that this is crossing iframes so the object has been serialized and deserialized.  It can be used for passing data but not functions.

##### Closing the modal
The modal add-in is responsible for triggering the close with the `closeModal` function on the client.  It is able to pass context information back to the parent add-in:

```js
// Modal add-in rendered in full screen iframe
var client = new AddinClient({...});
client.closeModal({
  context: { /* arbitrary context object to pass to parent add-in */ }
});
```

The parent add-in can listen to the close event via the `modalClosed` Promise returned from `showModal`. The Promise will resolve when the modal is closed, and will include the context data returned from the modal:

```js
// Parent add-in launching a modal
var client = new AddinClient({...});
var modal = client.showModal({
  url: '<modal-addin-url>',
  context: { /* arbitrary context object to pass to modal */ }
});

modal.modalClosed.then((context) => {
  // Handle that the modal is closed.
  // Use the context data passed back from closeModal.
});
```
#### Navigating the parent page

The add-in can choose to navigate the parent page based on user interactions.  To do so, call the `navigate` method on the `AddinClient` object.  This function takes an object argument with property `url` for where to navigate.  A fully qualified url should be used.

```js
var client = new AddinClient({...});
client.navigate({ url: '<target_url>' });
```

#### Opening a BB Help tab

The add-in can instruct the parent page to display the Help tab, and specify which page to display. To do this, call the `openHelp` method on the `AddinClient` object. This function takes an object argument with property `helpKey` for the name of the help tab to display. A single .html file should be named.

```js
var client = new AddinClient({...});
client.openHelp({ helpKey: '<target_page>.html' });
```

## Authentication
SKY API add-ins support a single-sign-on (SSO) mechanism that can be used to correlate the Blackbaud user with a user in the add-in's native system.

The `AddinClient` provides a `getAuthToken` function for getting a short-lived "user identity token" from the host page.  This token is a signed value that is issued to the SKY API application and represents the Blackbaud user's identity.

The general flow is that when an add-in is instantiated, it can request a user identity token from the host page using the `getAuthtoken` function. The host page will return the user identity token to the add-in.  The add-in can then pass the token to its own backend, where it can be validated and used to look up a user in the add-in's native system. If a user mapping exists, then the add-in can present content to the user.  If no user mapping exists, the add-in can prompt the user to login.  Once the user's identity in the native system is known, the add-in can persist the user mapping so that on subsequent loads the user doesn't have to log in again (even across devices).

Note that the user identity token is a JWT that is signed by the SKY API OAuth 2.0 service, but it cannot be used to make calls to the SKY API.  In order to make SKY API calls, a proper SKY API access token must be obtained.

##### Getting the user identity token
The `getAuthToken` function will return a Promise which will resolve with the token value.

```js
var client = new AddinClient({...});
client.getAuthToken().then((token: string) => {
  // use the token.
  var userIdentityToken = token;
  . . .
});
```
##### Validating the token

After obtaining a user identity token from the host page, the add-in can pass the token to its own backend.  The backend should first validate the token against the SKY API OpenIDConnect endpoint in order to ensure that it hasn't expired or been altered in any way.  This validation step is required in order for the backend to trust the user identity token.

The OpenIDConnect configuration can be found at https://oauth2.sky.blackbaud.com/.well-known/openid-configuration.

Developers building add-ins in .NET can make use of a Blackbaud-provided library to assist with validating the user identity token. This library is distributed as a NuGet package named `Blackbaud.Addin.TokenAuthentication`.  The package wraps up the logic for validating the user identity token JWT, and can be found at https://www.nuget.org/packages/Blackbaud.Addin.tokenAuthentication.

The following C# code snippet shows how to use the `Blackbaud.Addin.TokenAuthentication` library to validate the raw JWT token value passed in from the add-in client:

```cs
// this represents the user identity token returned from getAuthToken()
var rawToken = "(raw token value)";

// this is the ID of the developer's SKY API application
var applicationId = "(some application ID)";

// create and validate the user identity token
UserIdentityToken uit;
try
{
    uit = await UserIdentityToken.ParseAsync(rawToken, applicationId);

    // if valid, the UserId property contains the Blackbaud user's ID
    var userId = uit.UserId;
}
catch (TokenValidationException ex)
{
    // process the exception
}
```

Once the token has been validated, the add-in's backend will know the Blackbaud user ID and can determine if a user mapping exists for a user in the add-in's system. If a mapping exists, then the add-in's backend can immediately present the content for the add-in. If no user mapping exists, the add-in can prompt the user to login.
