UserApp PhoneGap
================

This library extends the [UserApp](https://www.userapp.io/) JavaScript SDKs with functionality that facilitates use with [PhoneGap](http://phonegap.com/).

It extends the `UserApp` JavaScript object with methods to create and remove persistent tokens based on the device id.

## Install

Download the `phonegap.userapp.js` file or install with bower: `$ bower install userapp-phonegap`

## Use with the UserApp AngularJS SDK

Automatically sets up a persistent session at login, so that the user only has to sign in once.
Just include `phonegap.userapp.js` after `angularjs.userapp.js`, like this:

```html
<script src="js/angularjs.userapp.js"></script>
<script src="js/phonegap.userapp.js"></script>
```

## Use with the UserApp Ember.js SDK

Automatically sets up a persistent session at login, so that the user only has to sign in once.
Just include `phonegap.userapp.js` after `ember-userapp.js`, like this:

```html
<script src="js/ember-userapp.js"></script>
<script src="js/phonegap.userapp.js"></script>
```

## Use with the UserApp JavaScript SDK

Include `phonegap.userapp.js` after `userapp.client.js`, like this:

```html
<script src="js/userapp.client.js"></script>
<script src="js/phonegap.userapp.js"></script>
```

This will extend the `UserApp` object with the methods `setupPersistentToken(callback)` and `removePersistentToken(callback)`.
After a successful login, call `setupPersistentToken()` to create a persistent token and then set the SDK to use it instead.

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

## Example

See the [Ionic Example](https://github.com/userapp-io/userapp-ionic) for a demo app based on [Ionic](http://ionicframework.com/) (AngularJS + PhoneGap) and UserApp.

## Help

Contact us via email at support@userapp.io or visit our [support center](https://help.userapp.io). You can also see the [UserApp documentation](https://app.userapp.io/#/docs/) for more information.

## License

MIT, see LICENSE.
