# suchjs

> Provides essential jQuery-like methods for your evergreen browser, in under 200 lines of code. Such small.

The code is written in a modular enough way that pieces can be removed easily, if that's deemed necessary. Just grab the bits you need!

# API

A `suchjs` object is exposed in the global `window` object, with the following methods.

## `suchjs(selector)`

Query a DOM selector. Returns a plain DOM object.

## `Node.prototype` extensions

The `Node` prototype is extended for extra convenience.

### `Node.prototype.on(type, cb)`

Aliases `Node.prototype.addEventListener(type, cb)`.

### `Node.prototype.remove()`

Removes the node from its parent.

### `Node.prototype.txt(value)`

Gets or sets the node's `innerText`.

### `Node.prototype.html(value)`

Gets or sets the node's `innerHTML`.

### `Node.prototype.attr(name, value)`

Gets or sets an attribute on the node.

## `suchjs.atoa(a)`

Cast array-like object to array.

## `suchjs.format(pattern, ...args)`

Node-style `'%s'` pattern replacement.

```js
suchjs.format('%s great %s-like', 'such', 'node');
// <- 'such great node-like'
```

## `suchjs.async.waterfall(steps, done)`

Provided an array of functions, it executes each one in turn, invoking `done` when it's all over or one of the steps returns a truthy error argument. Usage:

```js
suchjs.async.waterfall([
  function (next) {
    console.log('such async');
    next(null, 'wow', 'amaze');
  },
  function (wow, amaze, next) {
    console.log(suchjs.format('Wow, many %s amazed', amaze));
    next(null, 123);
  }
], function (err, data) {
  // handle errors
  console.log(data);
});
```

## `suchjs.async.parallel(steps, done)`

Similar to waterfall, but the steps will be executed in parallel. Steps can be an array like in `waterfall`, or an object. If it's an object, `done` will receive an object of mapped results. If it's an array, you'll get an array of results in the same order as the `steps`.

## `suchjs.ajax(url, options, done)`

AJAX. An URL, has a few options. Calls `done` with arguments: `res, status, { headers, original: xhr }`.

Option|Description|Default
----|----|----
`method`|Request Method|`GET`
`headers`|Request Headers|`{}`
`responseType`|Response Type|`json`
`data`|Request Data, either `POST` parameters or `GET` query|`{}`

Response `Link` headers get parsed.

## `suchjs.get(url, options, done)`

Short hand `ajax` method that issues a `GET` request.

## `suchjs.post(url, options, done)`

Short hand `ajax` method that issues a `POST` request.

# License

MIT
