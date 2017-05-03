# Webpack/ES6 Seed

* This is a project skeleton for developing in ES6 with Webpack
* To setup, run npm install and start coding!
* Additional guide included if you are interested on the steps I followed to setup the environmnet for the seed project


## File Structure

```
project
│   README.md
|   package.json
│   webpack.config.js
|   node_modules  
│
└───build
│   │   index.html
|   |   app.bundle.js
|   |   app.bundle.js.map
|
└───src
    │   index.js
    |   index.scss
    └───app
        │   app.js
        └───components
```

### Install

```Terminal
npm install
```
stat coding!

### This is how I set up the project:

# Setup Guide

## Steps

In the project folder:

```Terminal
npm init
```

## Babel

```Terminal
npm install --save-dev babel-loader babel-core
npm install --save-dev babel-preset-env
npm install --save-dev babel-plugin-transform-runtime
npm install --save babel-runtime
```

Add in package.json:

```Json
  "babel": {
    "presets": [
      "env"
    ],
    "plugins": [
      ["transform-runtime", {
        "helpers": false,
        "polyfill": false,
        "regenerator": true,
        "moduleName": "babel-runtime"
      }]
    ]
  },
```

**presets-env:** If you want to use ES6

**plugins-transform-runtime:** Eliminates duplication of babel helper functions (increases performance)

## Webpack

```Terminal
npm install --save-dev webpack
npm install --save-dev style-loader
npm install --save-dev css-loader
npm install --save-dev sass-loader
npm install --save-dev node-sass
touch webpack.config.js
```

Add in webpack.config.js:

```Javascript
var path = require('path');

module.exports = {
  context: path.join(__dirname, 'src'),
  entry: {
    app: './index.js'
  },
  output: {
    path: path.join(__dirname, 'build'),
    filename: '[name].bundle.js'
  },
  devtool: 'source-map',
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader',
        exclude: /node-modules/
      },
      {
        test: /\.scss$/,
        use: [
          {
            loader: 'style-loader'
          },
          {
            loader: 'css-loader',
            options: {
              sourceMap: true
            }
          },
          {
            loader: 'sass-loader',
            options: {
              sourceMap: true
            }
          }
        ]
      }
    ]
  }
 }

```
**entry:** The file you want to convert

**output:** The converted file named app.bundle.js

**rules:** Sets the loaders

**source-map:** If you want to edit sass/css in devtools

Add build script in package.json

```Json
"scripts": {
  "build": "webpack"
}
```
Run build to create new files

```Terminal
npm run build
```

## Webpack Dev Server

```Terminal
npm install --save-dev webpack-dev-server
```

Add in webpack.config.js

```Javascript
  devServer: {
    contentBase: path.join(__dirname, 'build'),
    inline: true,
    stats: 'errors-only'
  }
```

Add script in package.json

```Json
"scripts": {
  "start": "webpack-dev-server --open"
}
```
Run script to start server

```Terminal
npm start
```
Open browser in url

http://localhost:8080/webpack-dev-server

## Final look

### package.json
```Json
{
  "name": "project-webpack",
  "version": "1.0.0",
  "description": "* This is a project skeleton for developing in ES6 with Webpack * To setup, run npm install and start coding! * Additional guide included if you are interested on the steps I followed to setup the environmnet for the seed project",
  "main": "webpack.config.js",
  "babel": {
    "presets": [
      "env"
    ],
    "plugins": [
      ["transform-runtime", {
        "helpers": false,
        "polyfill": false,
        "regenerator": true,
        "moduleName": "babel-runtime"
      }]
    ]
  },
  "scripts": {
    "start": "webpack-dev-server --open",
    "build": "webpack"
  },
  "repository": {
    "type": "git",
    "url": "git+https://github.com/jdiejim/Seed-project-webpack.git"
  },
  "author": "",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/jdiejim/Seed-project-webpack/issues"
  },
  "homepage": "https://github.com/jdiejim/Seed-project-webpack#readme",
  "devDependencies": {
    "babel-core": "^6.24.1",
    "babel-loader": "^7.0.0",
    "babel-plugin-transform-runtime": "^6.23.0",
    "babel-preset-env": "^1.4.0",
    "babel-runtime": "^6.23.0",
    "css-loader": "^0.28.1",
    "node-sass": "^4.5.2",
    "sass-loader": "^6.0.3",
    "style-loader": "^0.17.0",
    "webpack": "^2.4.1",
    "webpack-dev-server": "^2.4.5"
  }
}
```
### webpack.config.js

```Javascript
var path = require('path');

module.exports = {
  context: path.join(__dirname, 'src'),
  entry: {
    app: './index.js'
  },
  output: {
    path: path.join(__dirname, 'build'),
    filename: '[name].bundle.js'
  },
  devtool: 'source-map',
  module: {
    rules: [
      {
        test: /\.js$/,
        use: 'babel-loader',
        exclude: /node-modules/
      },
      {
        test: /\.scss$/,
        use: [
          {
            loader: 'style-loader'
          },
          {
            loader: 'css-loader',
            options: {
              sourceMap: true
            }
          },
          {
            loader: 'sass-loader',
            options: {
              sourceMap: true
            }
          }
        ]
      }
    ]
  },
  devServer: {
    contentBase: path.join(__dirname, 'build'),
    inline: true,
    stats: 'errors-only'
  }
}
```
