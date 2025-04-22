# Resource

Small class to help you organize data aggregation within your node app.

Internally is a convenience wrapper on top of [Asker](https://github.com/nodules/asker), which, for one's turn, provides a better interface to `http.request`.

## Features

 * async (using [Vow](https://github.com/dfilatov/jspromise) promises);
 * prepares request options (three configuration levels, default values);
 * handles different datatypes (text, xml and json are supported for now);
 * catches a little bit more errors than Asker itself (parsing errors mostly);
 * can integrate with your cache system;
 * can be used for any data aggregation, even without http requests (see usage examples below).

## Getting started, create your `Resource`

`service_resource.js`:

```javascript
var Resource = require('resource'),
    ServiceResource = Resource
        .create()
        // you MUST set path to modules with resources
        .setPath(__dirname + '/')
        // you MIGHT set environment config
        .setEnvConfig(require(__dirname + '/../configs/development'))
        // you MIGHT enable logging of succesful http requests
        .setRequestLogger(function(message) {
            console.log(message);
        })
        // you MIGHT provide your caching methods, see doc below
        .setCache(new Cache());
```

## Basic usage

### Create `Resource` instance

`checkmobile.js`:

```javascript
var CheckMobile = require('./service_resource').create(),
    extend = require('extend');

CheckMobile.cfg = {
    path : '/detect',
    timeout : 1000,
    dataType : 'xml'
};

CheckMobile.prototype.prepareRequestOpts = function(req) {
    var params = extend({}, Resource.prototype.prepareRequestOpts.call(this));

    params.query = {};

    [ 'x-wap-profile', 'user-agent', 'x-operamini-phone-ua' ]
        .forEach(function(name) {
            req.headers.hasOwnProperty(name) && (params.query[name] = req.headers[name]);
        });

    return params;
};

/**
 * Post processing of returned data
 * @param {Object} results Xamel's nodeset
 * @returns {String}
 */
CheckMobile.prototype.processResultData = function(results) {
    return results.$('yandex-mobile-info/name/text()');
};

module.exports = CheckMobile;
```

### Use `resource`

Somewhere in our application:

```javascript
var resource = require('./service_resource');
// ...
resource('checkmobile', req)
    .then(function(data) {
        res.data.isMobile = !! data;
    })
    .fail(function() {
        res.data.isMobile = false;
    })
    .always(function() {
        promise.fulfill();
    });
```

## Configurating resources

### Priority

Each `Resource` instance has an options hash, which is used to prepare an http request.
It is created from three sources. They are listed by priority from highest to lowest.

#### Invocation config

Contains options that we passed to `resource` when invoked a resource from our app.
For example, if data from a resource is mandatory only on some of the pages, we can pass `isMandatory` option only on these pages.

```javascript
var resource = require('./service_resource');
// ...
return resource('user_settings', {
        req : req,
        user : res.data.user,
        settings : params
    },
    {
        isMandatory : true
    })
    // ...
```

#### `Resource` instance config

Is what we provided when created a resource file. Remember `CheckMobile.cfg`?

#### Application config

If present, is a project-level environment config.
Is provided via static `setEnvConfig` method. Must contain hash like this:

```javascript
checkmobile : {
    host : 'phd.yandex.net'
}
// ...
```

### Configuration options

All parameters are optional.

#### Resource options

 * `{String} dataType='json'` type of data expected to return from http request. `xml`, `json` or `text`.
 * `{String} logId` Resource id for logging purposes. Defaults to the name of resource file.
 * `{Boolean} isMandatory=false` Whether resource is mandatory for an application. If true, resource rejects promise in case of errors. Otherwise, errors are logged, but promise is still resolved.

#### Asker options, see [documentation](https://github.com/nodules/asker).

 * `host`
 * `port`
 * `path`
 * `requestId`
 * `maxRetries`
 * `timeout`
 * `agent`
 * `query`
 * `allowGzip`

#### XML parsing options

Also you can pass [xamel options](https://github.com/nodules/xamel#xamelparsexml-options-callback) as `{Object} xml` param:

 * `{String} buildPath`
 * `{Boolean} trim=true`
 * `{Boolean} cdata=false`

```javascript
CheckMobile.cfg = {
    path : '/detect',
    timeout : 1000,
    dataType : 'xml',
    xml : {
        buildPath : 'root/trololo/text()',
        cdata : true,
        trim : false
    }
};
```

#### Cache options

`Resource` itself does not provide any caching mechanism. Mostly it encapsulates creation of cache keys and then uses your cache methods.

When creating your `Resource` class, `setCache` argument should be an `Object` with two methods: `get` and `set`.

`get` as the only argument must accept `{String} cacheKey`, which resource provides.
`set` must accept three arguments: `{String} cacheKey`, `{*} response` and `{Number} keyTTL`.

Then resources, that are set as cacheable, would be calling your cache methods themselves.

Usage in resources configuration:
```javascript
cache : {
    get : { keyTTL : 1000 * 60 * 60 },
    generation : '2'
}
```

`cache {Object}`
Container for cache options. If it's not provided or equals `false`, resource will not be cached.

`get {Object}`
Cache rules for a given resource method (default resource method is `get`), these are NOT rules for a get operation.
You can set different rules for different methods of your resource.

`keyTTL {Number}`
"Time to live" for a cache entry.

`generation {String}`
Cache generation. Useful for manual cache flushing.

### Prototype methods

Can be overridden in particular resources.

 * `{Function} prepareRequestOpts(queryParams Object)` Prepares options for asker. By default it creates a `GET` request from default options.
 * `{Function} processResultData(response Object)` Processes Asker's response. By default returns all data. Can be overriden to return only part of data, filter data or whatever else you need.
 * `{Function} processError(reason *)` Error handler. By default rejects promise. For a example, could be overriden to return some default data.

### Error handling

`Resource` produces errors using [Terror](http://npm.im/terror), so you can setup your own logger and use `error.log()` method for logging.

If you already use Terror and created a logger for Terror itself, you shouldn't setup it again for `ResourceError`.

`ResourceError` class is available via `require('resource').Error` property. So you can, for example, localize error messages or customize it in your own way.

## More usage examples

### Check unit tests!

https://github.yandex-team.ru/nodules/resource/tree/master/test

### Example w/o http request

```javascript
var BrowserCheck = require('./service_resource').create();
    detector = require('browser-detector').Detector;

BrowserCheck.prototype.get = function(req) {
    var ret = { isMobile : false },
        headers = {};

    [ 'x-wap-profile', 'user-agent', 'x-operamini-phone-ua' ]
        .forEach(function(name) {
            req.headers.hasOwnProperty(name) && (headers[name] = req.headers[name]);
        });

    ret.isMobile = detector.detectByHeaders(headers).isMobile === true;

    return ret;
};

module.exports = BrowserCheck;
```

### Providing multiple methods

#### Create resource

You can extend resource prototype with your own methods and call them via
common resource calling interface.

Most of our application methods are the same as default `get` method,
but may have different prepare/processing phases.
So you can use static method `Resource.method(name, pipeline)` to define
resource methods in two ways:
* method is a single function with default error processing via `Resource#processError`;
* method is a chain of the following phases:
    * `prepare` (default is `prepareRequestOpts`): takes `opts` argument from method call and prepares options for the following phases;
    * `action` (default is `makeRequest`): executes resource action (retrieves data from DB, HTTP service, files; puts data back to storage);
    * `process` (default is `processResultData`): prepares retrieved data for further usage;
    * `error` (default is `processError`): if any of the previous phases fails, then error phase will be called with an error as first argument.

```javascript
var UserSettings = require('./service_resource').create();

UserSettings.cfg = {
    logId : 'settings',
    timeout : 300
};

UserSettings
    // single function method
    .method('get', function(opts) {
        var results = {};
        // ...
        return results;
    })
    // pipeline description with default action,
    // process and error phases and custom prepare phase.
    .method('put', {
        prepare : function(opts) {
            return this.prepareRequestOpts(extend(opts, EXTRA));
        },
        action : null,  // use default action `makeRequest`
        process : null, // use default Resource `processResultData`
        error : null    // use default error handler `processError`

        // properties with `null` values are ommited
        // result will be the same. So they were kept
        // only as an example for definition and
        // can be avoided in production code.
    });

module.exports = UserSettings;
```

#### Use resource

```javascript
return resource('user_settings.put', {
        req : req,
        user : user,
        settings : settings
    })
    .then(function() {
        // ...
    })
    .fail(function() {
        // ...
    });
```
