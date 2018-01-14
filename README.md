<a title="Co.Koa on github" href="https://jaysaurus.github.io/Co.Koa">
<img alt="Co.Koa header" title="Co.Koa" style="margin: 0 15%; width: 70%" src="https://raw.githubusercontent.com/jaysaurus/Co.Koa/master/siteStrapCoKoa.png?sanitize=true" />
</a>

# co-koa-session-plugin

koa-session plugin with support for mongoose within the [Co.Koa MVC](http://cokoajs.com) environment.

This plugin (available in the [Co.Koa MVC](http://cokoajs.com) from version @0.17.0 onwards)  aims to consolidate [koa-session](https://npmjs/package/koa-session) and a modified variation of [koa-session-mongoose](https://www.npmjs.com/package/koa-session-mongoose) into one easy-to-install module; thereby enabling secure session management that is handled via a session collection in your MongoDB database.

## installation

add co-koa-session-plugin to a Co.Koa project instance via:

```
npm i co-koa-session-plugin --save
```

within your app.js add the co-koa-session-plugin as a requirement and pass the SessionPlugin call as below:

```javascript
const fs = require('fs');
const SessionPlugin = require('co-koa-session-plugin');

if (fs.existsSync('./node_modules')) {
  const CoKoa = require('co-koa-core');
  try {
    const coKoa = CoKoa(__dirname).launch(SessionPlugin()); // <= HERE!
    ...
```

The `SessionPlugin` can optionally be called with a configuration object.  The properties of this object are described below:

```javascript
const coKoa =
  CoKoa(__dirname).launch(
    SessionPlugin({
      name: ... // the name of the collection (default is "Session")
      expires: ... // the amount of time in seconds until the session expires
    }));
```

## Use

In a controller, your session object is exposed as below:

```javascript
async 'GET /session' (ctx) {
  const { session } = ctx;
  let n = session.views || 0;
  session.views = ++n;
  ctx.body = `${n} view(s)`;
}
```

for more information on sessions, please see: [koa-session](https://npmjs/package/koa-session).
