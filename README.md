# Ember Data Adapter for parse-server

An [Ember Data](https://github.com/emberjs/data) plugin built to use the [Parse REST API](http://parseplatform.github.io/docs/rest/guide/). This is a full Ember implementation against the parse-server REST API without the use of the Parse JavaScript SDK.

If you are not familiarized with the new open source project [parse-server](https://github.com/ParsePlatform/parse-server), you should visit the project page first.

## Features

##### EmberParseAdapter.Serializer

* Provides the translation of objectId to id for identity mapping.
* Provides encoding of hasMany associations to arrays of [Parse Pointer objects](http://parseplatform.github.io/docs/rest/guide/#arrays).

##### EmberParseAdapter.Adapter

* Implements the persistence layer to parse-server by extending the Ember Data REST Adapter.
* Provides a `sessionToken` property which can set a session token.

##### EmberParseAdapter.ParseUser

Is stored at the special user endpoint at parse-server.

* Signup
* Login
* Logout
* Request password reset
* Request current user

##### EmberParseAdapter.Transforms

* Provides transforms for date, file and geo types at parse-server.

## Get started

You'll need to run [parse-server](https://github.com/ParsePlatform/parse-server) on your own. After this you will have to provide:

* The url of your parse-server ("http://localhost:1337" is the default value)
* The URL prefix of your Parse API ("parse" is the default value)
* The ID of your application
* The REST API Key of your application (only if you configure parse-server to require it)

You will need these to configure the ParseAdapter via entries in the `config/environment.js` file:

```javascript
var ENV = {
  ...

  APP: {
    parseUrl: '<THE URL OF THE PARSE SERVER HERE>',
    parseNamespace: '<THE URL PREFIX OF THE API HERE>',
    applicationId: '<YOUR APP ID HERE>',
    restApiId: '<YOUR REST API KEY HERE>' // (only if you use a Parse.com account)
  }
};
```

Any model using this adapter will be stored on Parse. Create models
as you would normally:

```javascript
App.Post = DS.Model.extend({
  // Attributes can use normal transforms
  title: DS.attr('string'),
  body: DS.attr('string'),
  rate: DS.attr('number'),
  // Or there are special transforms for some data-types like files
  avatar: DS.attr('parse-file'),
  // There is a parse-date transform, but sometimes dates are just strings
  updatedAt: DS.attr('parse-date'),
  // ALWAYS refer to relationships as async, for now.
  user: DS.belongsTo('parse-user', {async: true})
});
```

## Installation

* `git clone` this repository
* `npm install`
* `bower install`

## Running

* `ember server`
* Visit your app at http://localhost:4200.

## Running Tests

* `npm test` (Runs `ember try:testall` to test your addon against multiple Ember versions)
* `ember test`
* `ember test --server`

## Building

* `ember build`

For more information on using ember-cli, visit [http://www.ember-cli.com/](http://www.ember-cli.com/).
