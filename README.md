##node-sass

[![Build Status](https://secure.travis-ci.org/andrew/node-sass.png?branch=master)](https://travis-ci.org/andrew/node-sass)

Node-sass is a library that provides binding for Node.js to libsass, the C version of the popular stylesheet preprocessor, Sass.

It allows you to natively compile .scss files to css at incredible speed and automatically via a connect middleware.

Find it on npm: <https://npmjs.org/package/node-sass>

## Install

    npm install node-sass

## Usage

```javascript
var sass = require('node-sass');
sass.render(scss_content, callback [, options]);
// OR
var css = sass.renderSync(scss_content [, options]);
```

### Options

The options argument is optional, though it's use is recommended. It support two attributes: `includePaths` and `outputStyle`.

#### includePaths
`includePaths` is an `Array` of path `String`s to look for any `@import`ed files. It is recommended that you use this option if you have **any** `@import` directives, as otherwise libsass may not find your depended-on files.

#### outputStyle
`outputStyle` is a `String` to determine how the final CSS should be rendered. Its value should be one of `'nested', 'expanded', 'compact', 'compressed'`.
[Important: currently the argument `outputStyle` has some problem which may cause the output css becomes nothing because of the libsass, so you should not use it now!]

### Examples

```javascript
var sass = require('node-sass');
sass.render('body{background:blue; a{color:black;}}', function(err, css){
  console.log(css)
}/*, { includePaths: [ 'lib/', 'mod/' ], outputStyle: 'compressed' }*/);
// OR
console.log(sass.renderSync('body{background:blue; a{color:black;}}')/*, { includePaths: [ 'lib/', 'mod/' ], outputStyle: 'compressed' }*/);
```

## Connect/Express middleware

Recompile `.scss` files automatically for connect and express based http servers

```javascript
var server = connect.createServer(
  sass.middleware({
      src: __dirname
    , dest: __dirname + '/public'
    , debug: true
    , outputStyle: 'compressed'
  }),
  connect.static(__dirname + '/public')
);
```

Heavily inspired by <https://github.com/LearnBoost/stylus>

## Rebuilding binaries

Node-sass includes pre-compiled binaries for popular platforms, to add a binary for your platform follow these steps:

Check out the project:

    git clone https://github.com/andrew/node-sass.git
    cd node-sass
    npm install
    npm install -g node-gyp
    git submodule init
    git submodule update
    node-gyp rebuild

Replace the prebuild binary with your newly generated one

    cp build/Release/binding.node precompiled/*your-platform*/binding.node

## Contributors
Special thanks to the following people for submitting patches:

Dean Mao
Brett Wilkins
litek
gonghao

### Note on Patches/Pull Requests

 * Fork the project.
 * Make your feature addition or bug fix.
 * Add documentation if necessary.
 * Add tests for it. This is important so I don't break it in a future version unintentionally.
 * Send a pull request. Bonus points for topic branches.

## Copyright

Copyright (c) 2013 Andrew Nesbitt. See [LICENSE](https://github.com/andrew/node-sass/blob/master/LICENSE) for details.
