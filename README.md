# api documentation for  [debug (v2.6.3)](https://github.com/visionmedia/debug#readme)  [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-debug.svg)](https://travis-ci.org/npmdoc/node-npmdoc-debug)
#### small debugging utility

[![NPM](https://nodei.co/npm/debug.png?downloads=true)](https://www.npmjs.com/package/debug)

[![apidoc](https://npmdoc.github.io/node-npmdoc-debug/build/screen-capture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-debug_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-debug/build..beta..travis-ci.org/apidoc.html)

![package-listing](https://npmdoc.github.io/node-npmdoc-debug/build/screen-capture.npmPackageListing.svg)



# package.json

```json

{
    "author": {
        "name": "TJ Holowaychuk",
        "email": "tj@vision-media.ca"
    },
    "browser": "./src/browser.js",
    "bugs": {
        "url": "https://github.com/visionmedia/debug/issues"
    },
    "component": {
        "scripts": {
            "debug/index.js": "browser.js",
            "debug/debug.js": "debug.js"
        }
    },
    "contributors": [
        {
            "name": "Nathan Rajlich",
            "email": "nathan@tootallnate.net",
            "url": "http://n8.io"
        },
        {
            "name": "Andrew Rhyne",
            "email": "rhyneandrew@gmail.com"
        }
    ],
    "dependencies": {
        "ms": "0.7.2"
    },
    "description": "small debugging utility",
    "devDependencies": {
        "browserify": "9.0.3",
        "chai": "^3.5.0",
        "concurrently": "^3.1.0",
        "coveralls": "^2.11.15",
        "eslint": "^3.12.1",
        "istanbul": "^0.4.5",
        "karma": "^1.3.0",
        "karma-chai": "^0.1.0",
        "karma-mocha": "^1.3.0",
        "karma-phantomjs-launcher": "^1.0.2",
        "karma-sinon": "^1.0.5",
        "mocha": "^3.2.0",
        "mocha-lcov-reporter": "^1.2.0",
        "rimraf": "^2.5.4",
        "sinon": "^1.17.6",
        "sinon-chai": "^2.8.0"
    },
    "directories": {},
    "dist": {
        "shasum": "0f7eb8c30965ec08c72accfa0130c8b79984141d",
        "tarball": "https://registry.npmjs.org/debug/-/debug-2.6.3.tgz"
    },
    "gitHead": "9dc30f8378cc12192635cc6a31f0d96bb39be8bb",
    "homepage": "https://github.com/visionmedia/debug#readme",
    "keywords": [
        "debug",
        "log",
        "debugger"
    ],
    "license": "MIT",
    "main": "./src/index.js",
    "maintainers": [
        {
            "name": "thebigredgeek",
            "email": "rhyneandrew@gmail.com"
        }
    ],
    "name": "debug",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git://github.com/visionmedia/debug.git"
    },
    "scripts": {},
    "version": "2.6.3"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module debug](#apidoc.module.debug)
1.  [function <span class="apidocSignatureSpan"></span>debug (namespace)](#apidoc.element.debug.debug)
1.  [function <span class="apidocSignatureSpan">debug.</span>coerce (val)](#apidoc.element.debug.coerce)
1.  [function <span class="apidocSignatureSpan">debug.</span>default (namespace)](#apidoc.element.debug.default)
1.  [function <span class="apidocSignatureSpan">debug.</span>disable ()](#apidoc.element.debug.disable)
1.  [function <span class="apidocSignatureSpan">debug.</span>enable (namespaces)](#apidoc.element.debug.enable)
1.  [function <span class="apidocSignatureSpan">debug.</span>enabled (name)](#apidoc.element.debug.enabled)
1.  [function <span class="apidocSignatureSpan">debug.</span>formatArgs (args)](#apidoc.element.debug.formatArgs)
1.  [function <span class="apidocSignatureSpan">debug.</span>humanize (val, options)](#apidoc.element.debug.humanize)
1.  [function <span class="apidocSignatureSpan">debug.</span>init (debug)](#apidoc.element.debug.init)
1.  [function <span class="apidocSignatureSpan">debug.</span>load ()](#apidoc.element.debug.load)
1.  [function <span class="apidocSignatureSpan">debug.</span>log ()](#apidoc.element.debug.log)
1.  [function <span class="apidocSignatureSpan">debug.</span>save (namespaces)](#apidoc.element.debug.save)
1.  [function <span class="apidocSignatureSpan">debug.</span>useColors ()](#apidoc.element.debug.useColors)
1.  object <span class="apidocSignatureSpan">debug.</span>colors
1.  object <span class="apidocSignatureSpan">debug.</span>formatters
1.  object <span class="apidocSignatureSpan">debug.</span>inspectOpts
1.  object <span class="apidocSignatureSpan">debug.</span>names
1.  object <span class="apidocSignatureSpan">debug.</span>skips

#### [module debug.formatters](#apidoc.module.debug.formatters)
1.  [function <span class="apidocSignatureSpan">debug.formatters.</span>O (v)](#apidoc.element.debug.formatters.O)
1.  [function <span class="apidocSignatureSpan">debug.formatters.</span>o (v)](#apidoc.element.debug.formatters.o)



# <a name="apidoc.module.debug"></a>[module debug](#apidoc.module.debug)

#### <a name="apidoc.element.debug.debug"></a>[function <span class="apidocSignatureSpan"></span>debug (namespace)](#apidoc.element.debug.debug)
- description and source-code
```javascript
function createDebug(namespace) {

  function debug() {
    // disabled?
    if (!debug.enabled) return;

    var self = debug;

    // set 'diff' timestamp
    var curr = +new Date();
    var ms = curr - (prevTime || curr);
    self.diff = ms;
    self.prev = prevTime;
    self.curr = curr;
    prevTime = curr;

    // turn the 'arguments' into a proper Array
    var args = new Array(arguments.length);
    for (var i = 0; i < args.length; i++) {
      args[i] = arguments[i];
    }

    args[0] = exports.coerce(args[0]);

    if ('string' !== typeof args[0]) {
      // anything else let's inspect with %O
      args.unshift('%O');
    }

    // apply any 'formatters' transformations
    var index = 0;
    args[0] = args[0].replace(/%([a-zA-Z%])/g, function(match, format) {
      // if we encounter an escaped % then don't increase the array index
      if (match === '%%') return match;
      index++;
      var formatter = exports.formatters[format];
      if ('function' === typeof formatter) {
        var val = args[index];
        match = formatter.call(self, val);

        // now we need to remove 'args[index]' since it's inlined in the 'format'
        args.splice(index, 1);
        index--;
      }
      return match;
    });

    // apply env-specific formatting (colors, etc.)
    exports.formatArgs.call(self, args);

    var logFn = debug.log || exports.log || console.log.bind(console);
    logFn.apply(self, args);
  }

  debug.namespace = namespace;
  debug.enabled = exports.enabled(namespace);
  debug.useColors = exports.useColors();
  debug.color = selectColor(namespace);

  // env-specific initialization logic for debug instances
  if ('function' === typeof exports.init) {
    exports.init(debug);
  }

  return debug;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.coerce"></a>[function <span class="apidocSignatureSpan">debug.</span>coerce (val)](#apidoc.element.debug.coerce)
- description and source-code
```javascript
function coerce(val) {
  if (val instanceof Error) return val.stack || val.message;
  return val;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.default"></a>[function <span class="apidocSignatureSpan">debug.</span>default (namespace)](#apidoc.element.debug.default)
- description and source-code
```javascript
function createDebug(namespace) {

  function debug() {
    // disabled?
    if (!debug.enabled) return;

    var self = debug;

    // set 'diff' timestamp
    var curr = +new Date();
    var ms = curr - (prevTime || curr);
    self.diff = ms;
    self.prev = prevTime;
    self.curr = curr;
    prevTime = curr;

    // turn the 'arguments' into a proper Array
    var args = new Array(arguments.length);
    for (var i = 0; i < args.length; i++) {
      args[i] = arguments[i];
    }

    args[0] = exports.coerce(args[0]);

    if ('string' !== typeof args[0]) {
      // anything else let's inspect with %O
      args.unshift('%O');
    }

    // apply any 'formatters' transformations
    var index = 0;
    args[0] = args[0].replace(/%([a-zA-Z%])/g, function(match, format) {
      // if we encounter an escaped % then don't increase the array index
      if (match === '%%') return match;
      index++;
      var formatter = exports.formatters[format];
      if ('function' === typeof formatter) {
        var val = args[index];
        match = formatter.call(self, val);

        // now we need to remove 'args[index]' since it's inlined in the 'format'
        args.splice(index, 1);
        index--;
      }
      return match;
    });

    // apply env-specific formatting (colors, etc.)
    exports.formatArgs.call(self, args);

    var logFn = debug.log || exports.log || console.log.bind(console);
    logFn.apply(self, args);
  }

  debug.namespace = namespace;
  debug.enabled = exports.enabled(namespace);
  debug.useColors = exports.useColors();
  debug.color = selectColor(namespace);

  // env-specific initialization logic for debug instances
  if ('function' === typeof exports.init) {
    exports.init(debug);
  }

  return debug;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.disable"></a>[function <span class="apidocSignatureSpan">debug.</span>disable ()](#apidoc.element.debug.disable)
- description and source-code
```javascript
function disable() {
  exports.enable('');
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.enable"></a>[function <span class="apidocSignatureSpan">debug.</span>enable (namespaces)](#apidoc.element.debug.enable)
- description and source-code
```javascript
function enable(namespaces) {
  exports.save(namespaces);

  exports.names = [];
  exports.skips = [];

  var split = (namespaces || '').split(/[\s,]+/);
  var len = split.length;

  for (var i = 0; i < len; i++) {
    if (!split[i]) continue; // ignore empty strings
    namespaces = split[i].replace(/\*/g, '.*?');
    if (namespaces[0] === '-') {
      exports.skips.push(new RegExp('^' + namespaces.substr(1) + '$'));
    } else {
      exports.names.push(new RegExp('^' + namespaces + '$'));
    }
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.enabled"></a>[function <span class="apidocSignatureSpan">debug.</span>enabled (name)](#apidoc.element.debug.enabled)
- description and source-code
```javascript
function enabled(name) {
  var i, len;
  for (i = 0, len = exports.skips.length; i < len; i++) {
    if (exports.skips[i].test(name)) {
      return false;
    }
  }
  for (i = 0, len = exports.names.length; i < len; i++) {
    if (exports.names[i].test(name)) {
      return true;
    }
  }
  return false;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.formatArgs"></a>[function <span class="apidocSignatureSpan">debug.</span>formatArgs (args)](#apidoc.element.debug.formatArgs)
- description and source-code
```javascript
function formatArgs(args) {
  var name = this.namespace;
  var useColors = this.useColors;

  if (useColors) {
    var c = this.color;
    var prefix = '  \u001b[3' + c + ';1m' + name + ' ' + '\u001b[0m';

    args[0] = prefix + args[0].split('\n').join('\n' + prefix);
    args.push('\u001b[3' + c + 'm+' + exports.humanize(this.diff) + '\u001b[0m');
  } else {
    args[0] = new Date().toUTCString()
      + ' ' + name + ' ' + args[0];
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.humanize"></a>[function <span class="apidocSignatureSpan">debug.</span>humanize (val, options)](#apidoc.element.debug.humanize)
- description and source-code
```javascript
humanize = function (val, options) {
  options = options || {}
  var type = typeof val
  if (type === 'string' && val.length > 0) {
    return parse(val)
  } else if (type === 'number' && isNaN(val) === false) {
    return options.long ?
			fmtLong(val) :
			fmtShort(val)
  }
  throw new Error('val is not a non-empty string or a valid number. val=' + JSON.stringify(val))
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.init"></a>[function <span class="apidocSignatureSpan">debug.</span>init (debug)](#apidoc.element.debug.init)
- description and source-code
```javascript
function init(debug) {
  debug.inspectOpts = util._extend({}, exports.inspectOpts);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.load"></a>[function <span class="apidocSignatureSpan">debug.</span>load ()](#apidoc.element.debug.load)
- description and source-code
```javascript
function load() {
  return process.env.DEBUG;
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.log"></a>[function <span class="apidocSignatureSpan">debug.</span>log ()](#apidoc.element.debug.log)
- description and source-code
```javascript
function log() {
  return stream.write(util.format.apply(util, arguments) + '\n');
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.save"></a>[function <span class="apidocSignatureSpan">debug.</span>save (namespaces)](#apidoc.element.debug.save)
- description and source-code
```javascript
function save(namespaces) {
  if (null == namespaces) {
    // If you set a process.env field to null or undefined, it gets cast to the
    // string 'null' or 'undefined'. Just delete instead.
    delete process.env.DEBUG;
  } else {
    process.env.DEBUG = namespaces;
  }
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.useColors"></a>[function <span class="apidocSignatureSpan">debug.</span>useColors ()](#apidoc.element.debug.useColors)
- description and source-code
```javascript
function useColors() {
  return 'colors' in exports.inspectOpts
    ? Boolean(exports.inspectOpts.colors)
    : tty.isatty(fd);
}
```
- example usage
```shell
n/a
```



# <a name="apidoc.module.debug.formatters"></a>[module debug.formatters](#apidoc.module.debug.formatters)

#### <a name="apidoc.element.debug.formatters.O"></a>[function <span class="apidocSignatureSpan">debug.formatters.</span>O (v)](#apidoc.element.debug.formatters.O)
- description and source-code
```javascript
O = function (v) {
  this.inspectOpts.colors = this.useColors;
  return util.inspect(v, this.inspectOpts);
}
```
- example usage
```shell
n/a
```

#### <a name="apidoc.element.debug.formatters.o"></a>[function <span class="apidocSignatureSpan">debug.formatters.</span>o (v)](#apidoc.element.debug.formatters.o)
- description and source-code
```javascript
o = function (v) {
  this.inspectOpts.colors = this.useColors;
  return util.inspect(v, this.inspectOpts)
    .replace(/\s*\n\s*/g, ' ');
}
```
- example usage
```shell
n/a
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
