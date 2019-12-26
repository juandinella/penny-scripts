# @juandinella/penny-scripts

[![npm version](https://badge.fury.io/js/%40juandinella%2Fpenny-scripts.svg)](https://badge.fury.io/js/%40juandinella%2Fpenny-scripts)
[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)

A highly shareable and customizable webpack config.

## Features

- Dynamic Imports (Code Splitting)
- ES2017+
- JSX
- Linting via `@juandinella/eslint-config`
- Parsing all js (ours and vendor, vendor is cached though)
- Sourcemaps for debugging
- Tree-Shaking
- Extend and customize the underlying config

## Getting Started FAST!

```sh
npm install --dev @juandinella/penny-scripts
```

```sh
npx penny-scripts development
```

:fire:

We have a set of opinions towards how the files should look like for it to be a zero-config situation.

```
# Your project root
.
├── dist
│   └── assets
│       └── js
│           └── main.js # Compiled file
└── src
    └── assets
        └── js
            └── index.js # Your starting point
```

That is to be compliant with the defaults we were using on our `generator-frontend` package, however this is easy to customize.

## Node

Create an `index.js` with the following:

```js
const { compiler } = require("@juandinella/penny-scripts");

// Options are development, production or debug
const mode = "development";
console.log(`Compiling in ${mode} mode...`);

compiler(mode)
  .then(() => console.log(`All done!!`))
  .catch(e => console.log(e));
```

You can now run `node index` to get your JS compiled.

## Gulp

```js
const gulp = require("gulp");
const { compiler } = require("@juandinella/penny-scripts");

gulp.task("start", () => compiler("development"));
gulp.task("build", () => compiler("production"));

gulp.task("default", gulp.series("start"));
```

## Customizing the underlying config

To customize your setup you need to create a `scripts.config.js` file at the root of your project that file will be a function that takes 2 parameters:

- config (the default config) [See Webpack Config](https://webpack.js.org/configuration/)
- webpack (a webpack instance so you can use plugins and whatever)

`scripts.config.js`

```js
module.exports = function(config, webpack) {
  // tweak away esketit

  // Always return the config
  return config;
};
```
