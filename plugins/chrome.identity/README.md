# chrome.identity Plugin

This plugin provides OAuth2 authentication for Android and iOS.

On Android, this plugin uses Google Play Services; on iOS, it uses InAppBrowser.

## Status

Stable on Android; alpha on iOS.

## Reference

The API reference is [here](http://developer.chrome.com/apps/identity.html); a description of how to use the API is [here](http://developer.chrome.com/apps/app_identity.html).

## Preparing Your Application

### Android

You will need to register your application in the [Google Cloud Console](https://cloud.google.com/console).  Create a project.

On the left sidebar, navigate to "APIs & Auth" > "Registered Apps".  Click the red `Register App` button.

Register your app as an "Android" app.  This requires a package name and a SHA1 fingerprint.  To obtain the fingerprint, enter the following the command in a console window:

    keytool -exportcert -alias androiddebugkey -keystore ~/.android/debug.keystore -list -v

(On Windows, replace `~` with `%USERPROFILE%`.)

You will be prompted for a password, which is `android`.

This process will yield a client id, but no action is required with it (unlike for iOS).

### iOS

For iOS, first follow the instructions [here](https://developers.google.com/+/mobile/ios/getting-started).

**Note:** Skip step 2, part 7; you will instead put your client id in your manifest (as shown in the "Updating Your Manifest" section).

Next, in Xcode, click on the project in the left sidebar and navigate to the `Build Phases` tab.  In the `Compile Sources` section, remove `OpenInChromeController.m`.

## Updating Your Manifest

Your manifest needs to be updated to include your client id and scopes.  In a Mobile Chrome App (ie. an app created using mca.js), this is done in manifest.json as follows:

    "oauth2": {
      "client_id": "YOUR_IOS_CLIENT_ID",
      "scopes": [
        "SCOPE_1",
        "SCOPE_2",
        "SCOPE_3"
      ]
    },

When using this plugin outside the context of a Mobile Chrome App, this information must be provided using `chrome.runtime.setManifest`:

    chrome.runtime.setManifest({
      oauth2: {
        client_id: 'YOUR_IOS_CLIENT_ID',
        scopes: [ 'SCOPE_1', 'SCOPE_2', 'SCOPE_3' ]
      }
    });

## Playing With Google APIs

The [Google APIs Explorer](https://developers.google.com/apis-explorer/) is a useful tool for determining required scopes and testing various API use cases.
