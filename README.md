## Brick.JS

A fully modular MVC web application framework based on [Express.js][express]. 


### Features

* Modular Web Development. Each **module** contains: css, html, js, and a server controller.
* Isolated CSS. CSS is prefixed and applied to the corresponding html.
* Isolated Client-side JS. A minimal JS modularization/loading is done for each module.
* Minimal resource(CSS/JS) difference between development/production environment

### The Demo

[harttle/brick-demo][demo] is a minimal demo project for brick.js. 

### Minimal Usage

Install brick.js as well as a template engine:

```bash
npm install --save brick.js brick-hbs
```

```javascript
var brickJs = require('brick.js');
var hbs = require('brick-hbs');

var app = express();

var brk = brickJs({
    root: path.join(__dirname, 'modules'),
    engine: hbs.brick()
});

app.use('/', brk.express);
```

### Tutorial

* [How to create a simple module?][simple-module]
* [How to add CSS and client-side JS?][css-and-js]
* [How to customize the error page?][error-page]

For all usage and contribute guide, see: [brick.js wiki][wiki]

### Options

#### Full Usage

```javascript
var brk = brickJs({
    root: path.join(__dirname, 'modules'),
    engine: hbs.brick(),
    path: {
        svr: 'server.js',
        css: 'index.css',
        clt: 'client.js',
        tpl: 'index.html'
    },
    static: {
        css: {
            file: path.resolve(__dirname, '.build/site.css'),
            comment: '/* module: %s */',
            processor: require('brick-less')
        },
        js: {
            file: path.resolve(__dirname, '.build/site.js'),
            comment: '// module: %s'
        }
    }
});
```

#### root

Type: `String`

Default: `path.join(__dirname, 'modules')`

`root` is where the modules are located. Each module should be a folder consists of files specified by `path`.

#### engine

Type: `Object`

Default: `{render: (tpl, ctx, pctrl) => Promise.reject(new Error('ENOENGINE'))}`

Template engine for brick.js. Currently Available Template Engines:

* [brick-hbs][brick-hbs]: Handlebars template engine for brick.js
* [brick-liquid][brick-liquid]: Liquid template engine for brick.js

Template Engine Development Guide: [Template Engine Interface][tpl-contrib]

#### path.svr

Type: `String`

Default: `'server.js'`

Server controller file name in module folder, see [`root`](#root).

#### path.clt

Type: `String`

Default: `'client.js'`

Client JS file name. See [`path.svr`](#pathsvr).

#### path.tpl

Type: `String`

Default: `'index.html'`

HTML template file name. See [`path.svr`](#pathsvr).

#### path.css

Type: `String`

Default: `'index.css'`

CSS/LESS file name. See [`path.svr`](#pathsvr).

#### static.css.file

Type: `String`

Default: `false`

Absolute filepath for brick.js to save the generated css, this file is for build/deploy usage.
When set to `false`, the css file won't be saved. 

Note: this file can be conflict with `express.static` directory. Keep the URLs different.

#### static.css.comment

Type: `String`

Default: `'/* module: %s */'`

Comment before each module's css in the generated css file. 

Note: `%s` is the module name ([param-cased][param-case]).

#### static.css.processor

Type: `Function`

Default: prefix and combine css files

CSS pre-processor (like LESS/SASS) wrapper. [harttle/brick-less][brick-less] is available.

#### static.js.file

Type: `String`

Default: `false`

See `static.css.file`.

#### static.js.comment

Type: `String`

Default: `'// module: %s'`

See `static.css.comment`.

[express]: http://expressjs.com/en/index.html 
[simple-module]: https://github.com/harttle/brick.js/wiki/a-simple-module
[brick-hbs]: https://github.com/harttle/brick-hbs
[brick-liquid]: https://github.com/harttle/brick-liquid
[demo]: https://github.com/harttle/brick-demo
[wiki]: https://github.com/harttle/brick.js/wiki
[error-page]: https://github.com/harttle/brick.js/wiki/customize-error-page
[css-and-js]: https://github.com/harttle/brick.js/wiki/css-and-js
[param-case]: https://github.com/blakeembrey/param-case
[tpl-contrib]: https://github.com/harttle/brick.js/wiki/Template-Engine-Interface
[brick-less]: https://github.com/harttle/brick-less
