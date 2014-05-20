UserApp PhoneGap
================

This library extends the [UserApp](https://www.userapp.io/) JavaScript SDKs with functionality that facilitates use with [PhoneGap](http://phonegap.com/).

It extends the `UserApp` JavaScript object with methods to create and remove persistent tokens based on the device id. It also makes sure that the token gets saved in localStorage instead of a cookie. Social Login will be made through the [InAppBrowser](http://docs.phonegap.com/en/3.0.0/cordova_inappbrowser_inappbrowser.md.html) plugin instead of a redirect.

## Install

Download the `phonegap.userapp.js` file or install with bower: `$ bower install userapp-phonegap`

## Use with the UserApp AngularJS SDK

Use this library with the [AngularJS SDK](https://app.userapp.io/#/docs/libs/angularjs/) and it will automatically set up a persistent session at login, so that the user only has to sign in once. Just include `phonegap.userapp.js` after `angularjs.userapp.js`, like this:

```html
<script src="js/userapp.client.js"></script>
<script src="js/angularjs.userapp.js"></script>
<script src="js/phonegap.userapp.js"></script>
```

For Social Login you need the [InAppBrowser](http://docs.phonegap.com/en/3.0.0/cordova_inappbrowser_inappbrowser.md.html) plugin:

    $ cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git

## Use with the UserApp Ember.js SDK

Use this library with the [Ember.js SDK](https://app.userapp.io/#/docs/libs/emberjs/) and it will automatically set up a persistent session at login, so that the user only has to sign in once. Just include `phonegap.userapp.js` after `ember-userapp.js`, like this:

```html
<script src="js/userapp.client.js"></script>
<script src="js/ember-userapp.js"></script>
<script src="js/phonegap.userapp.js"></script>
```

For Social Login you need the [InAppBrowser](http://docs.phonegap.com/en/3.0.0/cordova_inappbrowser_inappbrowser.md.html) plugin:

    $ cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git

## Use with the UserApp JavaScript SDK

Include `phonegap.userapp.js` after `userapp.client.js`, like this:

```html
<script src="js/userapp.client.js"></script>
<script src="js/phonegap.userapp.js"></script>
```

This will extend the `UserApp` object with the methods `setupPersistentToken(callback)`, `removePersistentToken(callback)`, and `oauthHandler(url, callback)`.
After a successful login, call `setupPersistentToken()` to create a persistent token and then set the [JavaScript SDK](https://app.userapp.io/#/docs/libs/javascript/) to use that token:

```javascript
UserApp.User.login(user, function(error, result) {
  if (result) {
    if (result.locks && result.locks.length > 0) {
      UserApp.setToken(null);
    } else {
      UserApp.setupPersistentToken(function(error, token) {
        if (token) {
          UserApp.setToken(token.value);
        } else {
          UserApp.setToken(null);
        }
      });
    }
  }
});
```

And use the method `removePersistentToken()` to destroy the persistent session.

```javascript
UserApp.removePersistentToken(function(error) {
  UserApp.setToken(null);
});
```

Use the method `oauthHandler()` to open a new browser with an authorization url and then return a persistent token. If the token is `null`, the browser was closed.

```javascript
UserApp.OAuth.getAuthorizationUrl({ provider_id: 'facebook' }, function(error, result) {
  if (!error) {
    UserApp.oauthHandler(result.authorization_url, function(token) {
      if (token) {
        // the user is logged in with the persistent token 'token'
      }
    }); 
  }
});
```

This requires the [InAppBrowser](http://docs.phonegap.com/en/3.0.0/cordova_inappbrowser_inappbrowser.md.html) plugin:

    $ cordova plugin add https://git-wip-us.apache.org/repos/asf/cordova-plugin-inappbrowser.git

## Example

See the [Ionic Example](https://github.com/userapp-io/userapp-ionic) for a demo app based on [Ionic](http://ionicframework.com/) (AngularJS + PhoneGap) and UserApp.

## Help

Contact us via email at support@userapp.io or visit our [support center](https://help.userapp.io). You can also see the [UserApp documentation](https://app.userapp.io/#/docs/) for more information.

## License

MIT, see LICENSE.
