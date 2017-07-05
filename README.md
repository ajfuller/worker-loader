[![npm][npm]][npm-url]
[![node][node]][node-url]
[![deps][deps]][deps-url]
[![test][test]][test-url]
[![coverage][cover]][cover-url]
[![chat][chat]][chat-url]

<div align="center">
  <a href="https://github.com/webpack/webpack">
    <img width="200" height="200" src="https://cdn.rawgit.com/webpack/media/e7485eb2/logo/icon.svg">
  </a>
  <h1>Worker Loader</h1>
  <p>This loader registers the script as <a href="https://developer.mozilla.org/en-US/docs/Web/API/Web_Workers_API">Web Worker</a><p>
</div>


<h2 align="center">Install</h2>

```bash
npm i -D worker-loader
```

<h2 align="center"><a href="https://webpack.js.org/concepts/loaders">Usage</a></h2>

**App.js**
```js
import Worker from 'worker-loader!./Worker.js'

const worker = new Worker()

worker.postMessage({ a: 1 })
worker.onmessage = function (event) {}

worker.addEventListener("message", function (event) {})
```

<h2 align="center">Options</h2>

|Name|Type|Default|Description|
|:--:|:--:|:-----:|:----------|
|**`name`**|`{String}`|`[name]`|Set a custom name for the output script|
|**`inline`**|`{Boolean}`|`false`|Inline the worker as a BLOB|
|**`fallback`**|`{Boolean}`|`false`|Require a fallback for non-worker supporting environments|

### `name`

To set a custom name for the output script, use the `name` parameter. The name may contain the string `[hash]`, which will be replaced with a content dependent hash for caching purposes.

**App.js**
```js
import Worker from 'worker-loader?name=WorkerName.[hash].js!./Worker.js'
```

### `inline`

You can also inline the worker as a BLOB with the `inline` parameter

**App.js**
```js
import Worker from 'worker-loader?inline!./Worker.js'
```

> ℹ️  Inline mode will also create chunks for browsers without support for inline workers, to disable this behavior just set `fallback` parameter as `false`

**App.js**
```js
import Worker from 'worker-loader?inline&fallback=false!./Worker.js'
```

### `fallback`

Require a fallback for non-worker supporting environments.

**App.js**
```js
import Worker from 'worker-loader?fallback=true!./Worker.js'
```

<h2 align="center">Examples</h2>

The worker file can import dependencies just like any other file.

**Worker.js**
```js
const _ = require('lodash')

const obj = { foo: 'foo' }

_.has(obj, 'foo')

// Post data to parent thread
self.postMessage({ foo: 'foo' })

// Respond to message from parent thread
self.addEventListener('message', (event) => console.log(event))  
```

### `Integrating with ES2015 Modules`

> ℹ️  You can even use ES2015 Modules if you have the [`babel-loader`](https://github.com/babel/babel-loader) configured.

**Worker.js**
```js
import _ from 'lodash'

const obj = { foo: 'foo' }

_.has(obj, 'foo')

// Post data to parent thread
self.postMessage({ foo: 'foo' })

// Respond to message from parent thread
self.addEventListener('message', (event) => console.log(event))
```

### `Integrating with TypeScript`

To integrate with TypeScript, you will need to define a custom module for the exports of your worker. You will also need to cast the new worker as the `Worker` type:

**typings/custom.d.ts**
```ts
declare module "worker-loader!*" {
  const content: any;
  export = content;
}
```

**App.ts**
```ts
import * as Worker from "worker-loader!./Worker.ts";

const worker: Worker = new Worker();
```

<h2 align="center">Maintainers</h2>

<table>
  <tbody>
    <tr>
      <td align="center">
        <a href="https://github.com/TrySound">
          <img width="150" height="150" src="https://avatars3.githubusercontent.com/u/5635476?v=3&s=150">
        </a>
        <br />
        <a href="https://github.com/TrySound">Bogdan Chadkin</a>
      </td>
      <td align="center">
        <a href="https://github.com/bebraw">
          <img width="150" height="150" src="https://github.com/bebraw.png?v=3&s=150">
          </br>
          Juho Vepsäläinen
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/d3viant0ne">
          <img width="150" height="150" src="https://github.com/d3viant0ne.png?v=3&s=150">
          </br>
          Joshua Wiens
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/sapegin">
          <img width="150" height="150" src="https://github.com/sapegin.png?v=3&s=150">
          </br>
          Artem Sapegin
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/michael-ciniawsky">
          <img width="150" height="150" src="https://github.com/michael-ciniawsky.png?v=3&s=150">
          </br>
          Michael Ciniawsky
        </a>
      </td>
      <td align="center">
        <a href="https://github.com/evilebottnawi">
          <img width="150" height="150" src="https://github.com/evilebottnawi.png?v=3&s=150">
          </br>
          Alexander Krasnoyarov
        </a>
      </td>
    </tr>
  <tbody>
</table>


[npm]: https://img.shields.io/npm/v/worker-loader.svg
[npm-url]: https://npmjs.com/package/worker-loader

[node]: https://img.shields.io/node/v/cache-loader.svg
[node-url]: https://nodejs.org

[deps]: https://david-dm.org/webpack-contrib/worker-loader.svg
[deps-url]: https://david-dm.org/webpack-contrib/worker-loader

[test]: http://img.shields.io/travis/webpack-contrib/worker-loader.svg
[test-url]: https://travis-ci.org/webpack-contrib/worker-loader

[cover]: https://codecov.io/gh/webpack-contrib/cache-loader/branch/master/graph/badge.svg
[cover-url]: https://codecov.io/gh/webpack-contrib/cache-loader

[chat]: https://img.shields.io/badge/gitter-webpack%2Fwebpack-brightgreen.svg
[chat-url]: https://gitter.im/webpack/webpack
