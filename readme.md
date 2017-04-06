
# Node Cookie

> Easily parse and write signed & encrypted cookies on Node.js HTTP requests.

<br />

<p align="center">
  <a href="http://i1117.photobucket.com/albums/k594/thetutlage/poppins-1_zpsg867sqyl.png">
    <img src="http://i1117.photobucket.com/albums/k594/thetutlage/poppins-1_zpsg867sqyl.png" width="600px" />
  </a>
</p>

<br />

---

[![NPM Version][npm-image]][npm-url]
[![Build Status][travis-image]][travis-url]
[![Appveyor][appveyor-image]][appveyor-url]


## See also

1. [node-req](https://npmjs.org/package/node-req)
2. [node-res](https://npmjs.org/package/node-res)

## Basic Setup

```javascript
const http = require('http')
const nodeCookie = require('node-cookie')

http.createServer(function (req, res) {

  // this will update set-cookie header on res object.
  nodeCookie.create(res, 'user', 'virk')

}).listen(3000)
```

## Signing cookies with a secret

```javascript
const http = require('http')
const nodeCookie = require('node-cookie')

http.createServer(function (req, res) {

  nodeCookie.create(res, 'user', 'virk', '16charlongsecret')

}).listen(3000)
```

## Signing & encrypting cookies with a secret

```javascript
const http = require('http')
const nodeCookie = require('node-cookie')

http.createServer(function (req, res) {

  nodeCookie.create(res, 'user', 'virk', '16charlongsecret', true)

}).listen(3000)
```

## Methods

### parse
Parses cookies from HTTP header `Cookie` into
a javascript object. Also it will unsign
and decrypt cookies encrypted and signed
by this library using a secret.

**Params**

| Param | Type | Required | Description |
|-----|-------|------|------|
| req | Object | Yes | &nbsp; |
| secret  | String | No | &nbsp; |
| decrypt  | Boolean | No | &nbsp; |

**Returns**
Object

**Example**
```js
nodeCookie.parse(req)

// or if cookies were signed when writing
nodeCookie.parse(req, 'SECRET')

// also if cookies where encrypted
nodeCookie.parse(req, 'SECRET', true)
```

----
### get
Returns value for a single cookie by its key. It is
recommended to make use of this function when you
want to pull a single cookie. Since the `parse`
method will eagerly unsign and decrypt all the
cookies.

**Params**

| Param | Type | Required | Description |
|-----|-------|------|------|
| req | Object | Yes | &nbsp; |
| key | String | Yes | &nbsp; |
| secret  | String | No | &nbsp; |
| decrypt  | Boolean | No | &nbsp; |
| cookies  | Object | No | Use existing cookies object over re-parsing them from the header. |

**Returns**
Mixed

**Example**
```js
nodeCookie.get(req, 'sessionId')

// or if session cookie was signed
nodeCookie.get(req, 'sessionId', 'SECRET')

// also or if session cookie was encrypted
nodeCookie.get(req, 'sessionId', 'SECRET', true)
```

----
### create
Write cookie to the HTTP response object. It will append
duplicate cookies to the `Set-Cookie` header, since
browsers discard the duplicate cookies by themselves

**Params**

| Param | Type | Required | Description |
|-----|-------|------|------|
| res | Object | Yes | &nbsp; |
| key | String | Yes | &nbsp; |
| value | * | Yes | &nbsp; |
| options  | Object | No | &nbsp; |
| secret  | String | No | &nbsp; |
| encrypt  | Boolean | No | &nbsp; |

**Returns**
Void

**Example**
```js
nodeCookie.create(res, 'sessionId', 1)

// sign session id
nodeCookie.create(res, 'sessionId', 1, {}, 'SECRET')

// sign and encrypt session id
nodeCookie.create(res, 'sessionId', 1, {}, 'SECRET', true)
```

----
### clear
Clears the cookie from browser by setting it's expiry
in past. This is required since there is no other
way to instruct the browser to delete a cookie.

Also this method will override the `expires` value on
the options object.

**Params**

| Param | Type | Required | Description |
|-----|-------|------|------|
| res | Object | Yes | &nbsp; |
| key | String | Yes | &nbsp; |
| options  | Object | No | &nbsp; |

**Returns**
Void

**Example**
```js
nodeCookie.clear(res, 'sessionId')
```

----

[appveyor-image]: https://ci.appveyor.com/api/projects/status/github/poppinss/node-req?branch=master&svg=true&passingText=Passing%20On%20Windows
[appveyor-url]: https://ci.appveyor.com/project/thetutlage/node-cookie

[npm-image]: https://img.shields.io/npm/v/node-cookie.svg?style=flat-square
[npm-url]: https://npmjs.org/package/node-cookie

[travis-image]: https://img.shields.io/travis/poppinss/node-cookie/master.svg?style=flat-square
[travis-url]: https://travis-ci.org/poppinss/node-cookie
