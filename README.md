# Feathers Hooks

[![Build Status](https://travis-ci.org/feathersjs/feathers-hooks.png?branch=master)](https://travis-ci.org/feathersjs/feathers-hooks)

> Middleware for Feathers service methods

## Getting Started

`feathers-hooks` allow to register composable middleware functions **before** or **after** a Feathers service method executes. This makes it easy to decouple things like authorization and pre- or post processing from your service logic.

To install from [npm](https://www.npmjs.com/package/feathers-hooks), run:

```bash
$ npm install feathers-hooks --save
```

Then, to use the plugin in your Feathers app:

```javascript
var feathers = require('feathers');
var hooks = require('feathers-hooks');

var app = feathers().configure(hooks());
```

Then, you can register the hook for a service:

```javascript
// User service
import service from 'feathers-memory';

export default function(){
  const app = this;

  let myHook = function(options) {
    return function(hook) {
      console.log('My custom hook ran!');
    }
  }

  // Initialize our service
  app.use('/users', service());

  // Get our initialize service to that we can bind hooks
  const userService = app.service('/users');

  // Set up our before hook
  userService.before({
    find: [myHook()]
  });
}
```

## Examples

The repository contains the following examples:

- [authorization.js](https://github.com/feathersjs/feathers-hooks/blob/master/examples/authorization.js) - A simple demo showing how to use hooks for authorization (and post-processing the results) where the user is set via a `?user=username` query parameter.
- [timestamp.js](https://github.com/feathersjs/feathers-hooks/blob/master/examples/timestamp.js) - A demo that adds a `createdAt` and `updatedAt` timestamp when creating or updating a Todo using hooks.

## Documentation
Please refer to the [Feathers hooks documentation](http://docs.feathersjs.com/hooks/readme.html) for more details on:

- The philosophy behind hooks
- How you can use hooks
- How you can chain hooks using Promises
- Params that are available in hooks
- Hooks that are bundled with feathers and feathers plugins

## Changelog

__1.0.0__

- Make `app` available inside the `hook` object ([#34](https://github.com/feathersjs/feathers-hooks/pull/34))

__0.6.0__

- Prevent next from being called multiple times ([#27](https://github.com/feathersjs/feathers-hooks/pull/27))
- Migrate to ES6 and new plugin infrastructure ([#26](https://github.com/feathersjs/feathers-hooks/pull/26))

__0.5.0__

- Make sure hooks and service methods keep their context ([#17](https://github.com/feathersjs/feathers-hooks/issues/17))
- Refactoring to fix hook execution order and all-hooks ([#16](https://github.com/feathersjs/feathers-hooks/issues/16))
- Arrays of Hooks are running in reverse order ([#13](https://github.com/feathersjs/feathers-hooks/issues/13))
- Before all and after all hooks ([#11](https://github.com/feathersjs/feathers-hooks/issues/11))
- Better check for .makeArguments id ([#15](https://github.com/feathersjs/feathers-hooks/issues/15))
- Remove Feathers peer dependency ([#12](https://github.com/feathersjs/feathers-hooks/issues/12))

__0.4.0__

- Allows hooks to be chained in an array ([#2](https://github.com/feathersjs/feathers-hooks/issues/2))

__0.3.0__

- Allows hooks to return a promise ([#3](https://github.com/feathersjs/feathers-hooks/issues/3), [#4](https://github.com/feathersjs/feathers-hooks/issues/4))

__0.2.0__

- API change to use hook objects instead of function parameters ([#1](https://github.com/feathersjs/feathers-hooks/issues/1))

__0.1.0__

- Initial release

## Author

- [David Luecke](https://github.com/daffl)

## License

Copyright (c) 2014 David Luecke

Licensed under the [MIT license](LICENSE).
