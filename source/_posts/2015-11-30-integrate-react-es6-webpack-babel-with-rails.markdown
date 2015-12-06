---
layout: post
title: Integrate React, ES6, Webpack and Babel with Rails
date_string: 30 November 2015
--- 

### Roll your own

If you have got two projects using the same functionality, then write a **Rubygem** to promote code reuse and modularity. Writing a gem is not a new thing. In fact, there are 6,710,940,000 gems and counting, as per the [rubygems homepage](https://rubygems.org/). 

Years ago Jamis Buck said in one of his blogs that if you don't understand the inner workings of a gem, don't use it as a dependency. Very fair comment indeed! I'm guilty of using the gems without really knowing their inner workings. To be honest, as a modern day programmer with a constant client expectation to deliver solutions, it's okay to take your eyes of the ball. 

However, I decided to make amendments when it came to integrating a react app into rails. I wanted to learn and fix the issues that comes with integrating and therefore, decided to start it from scratch. If you wish to use, there are a couple of nice integrate react with rails gems out there, namely, [react_on_rails](https://github.com/shakacode/react_on_rails) and [react-rails](https://github.com/reactjs/react-rails).


### What are we going to do

Recently, I have crossed over to the Javascript world and been doing a lot of React, ES6 (with babel) and webpack and I wanted to use the same ideas in a Rails project. 

There are a few things to keep in mind:

1. A react component will serve as the client talking to the rails as a backend.
2. The rails will be used a backend.
3. It's not an isomorphic application meaning there will be no server-side rendering of react components.
4. It should play nicely with rails asset pipeline.

As part of this article, we are going to set-up a react app in both development and production-mode that will play nicely with a rails app.

### Setting up a rails app

As a seasoned rails developer, I expect you guys to know how to do this.

### Setting up a react app

* Create a directory called `client` at the same level as the `app`.
* Create a file called `package.json` in the `client` directory. Package.json is to npm what Gemfile is to Bundler. Copy the following contents into the client/package.json. Most of it is pretty self-explanatory except the scripts section. Npm allows you to create these tasks inside the scripts section runnable from the command line via `npm run` command. Under `scripts`, `start` starts a webpack dev server useful for reloading the app whilst working in development. `build` is for building the app locally and uses the default webpack config and finally, `build:prod` builds the final distributable js file using webpack's production config.

```
{
  "name": "react-app",
  "version": "0.0.1",
  "description": "React App",
  "scripts": {
    "start": "webpack-dev-server --content-base dist/ --port 9999",
    "build": "./node_modules/webpack/bin/webpack.js --progress",
    "build:prod": "./node_modules/webpack/bin/webpack.js -p --progress --config webpack.production.config.js"
  },
  "dependencies": {
    "react": "^0.14.2",
    "react-dom": "^0.14.2"
  },
  "devDependencies": {
    "babel-core": "^6.0.20",
    "babel-eslint": "^4.1.5",
    "babel-loader": "^6.0.1",
    "babel-preset-es2015": "^6.0.15",
    "babel-preset-react": "^6.0.15",
    "babel-preset-stage-0": "^6.0.15",
    "eslint": "^1.8.0",
    "eslint-loader": "^1.1.1",
    "eslint-plugin-react": "^3.6.3",
    "html-webpack-plugin": "^1.6.2",
    "react-hot-loader": "^1.3.0",
    "webpack": "^1.12.2",
    "webpack-dev-server": "^1.12.1"
  }
}
```

* Create `webpack.base.config.js` in the `client` directory with the following contents:* 

```
var webpack = require('webpack');

module.exports = {
    entry: './src/js/app.js',
    output: {
        path: '../app/assets/javascripts/',
        filename: "bundle.js"
    },
    module: {
        preLoaders: [
            {
                test: /(\.js$)/,
                exclude: /node_modules/,
                loader: "eslint-loader"
            }
        ],
        loaders: [
            {
                test: /\.js$/,
                exclude: /node_modules/,
                loader: "babel-loader",
                query: {
                   presets: [ "react", "es2015", "stage-0" ]
                }
            }
        ]
    },
    eslint: {
        configFile: '.eslintrc'
    },
    plugins: [
        new webpack.NoErrorsPlugin()
    ]
}

```
	

* Create `webpack.config.js`  in the `client` directory with the following contents. This is the default config used by webpack.

```
var webpack = require('webpack'),
    config = require('./webpack.base.config.js');

config.entry = [
    'webpack-dev-server/client?http://0.0.0.0:9999',
    config.entry
];

config.output = {
    path: config.output.path,
    filename: config.output.filename
};

module.exports = config;

```

* Finally, create `webpack.production.config.js`  in the `client` directory with the following contents. This is mainly used for creating a production ready distributable bundle. It is invoked with a `-p` option at the command line to trigger automatic minification.

```
var webpack = require('webpack'),
    config = require('./webpack.base.config.js');

config.entry = [
    config.entry
];

config.output = {
	path: config.output.path,
    filename: config.output.filename
};

module.exports = config;

```

* Create a directory called `src/js` in the `client` directory.

* In the `src/js` directory, create a file called `app.js`. This is the entry file for webpack. Entry file is the file webpack uses to workout all the other dependencies that it needs to bundle up in the final distributable file. 

* The `app.js` file should have the following contents. This is the entry point for the app. Here it's rendering the react app in a dom node with the id `react-app`. Make sure a dom node with the same id exists in the layout file of your rails app, otherwise, react will have no place to mount the app.

```
import React from 'react'
import ReactDOM from 'react-dom'
import App from './components/App.react'

ReactDOM.render(
    <App />,
    document.getElementById('react-app')
);
```

* One last thing, create the following directory, src/js/components and in there create a root react component called App.react.js with the following contents. As you can see, the `App` is written in ES6 classes and takes advantage of the modular dependency provided by ES6 out of the box.

```
import React, { Component, PropTypes } from 'react'

class App extends Component {
    render() {
        return (
            <div>
                <h1>React App</h1>
            </div>
        );
    }
}

export default App

```

### Workflow

* Open a terminal window and navigate to the client directory that we created above.
* Run `npm run build`. This will create a bundle.js (development version) and to `app/assets/javascripts` directory.
* Make sure to refer to it from the layout file. I added it to the `config/initializers/assets.rb` as a precompiled file:

```
Rails.application.config.assets.precompile += %w( bundle.js )
``` 

* Added it at the bottom of the layout file with a script tag to ensure the DOM node that react app depends upon is there before react's mounting kicks in.

* Opened the rails root page in a browser to check the react app is being mounted correctly and `React App` (the contents of the App.react.js component) is being rendered on the page.


### Phew, further investigation things!

* Firstly, you will see there is an error in the dev tools. The app still works fine. This means the at the time of the mount react didn't find the DOM node which seems bizzare because it works fine. I noticed removing the line of code that brings in `application.js` in your rails layout file fixes this issue.

```
Uncaught Error: Invariant Violation: _registerComponent(...): Target container is not a DOM element.
```


* You will also notice a lot of sock.js errors in the dev tools. This is because the in the webpack development config we've set it up to communicate with the local webpack dev server and update any changes to the app via websocket. I haven't quite worked out how the webpack-dev-server communication with this will work, so ignore those for now, or just build the bundle.js using webpack production config.


And, that's it!


**Update: 06 December 2015**

The following error

```
Uncaught Error: Invariant Violation: _registerComponent(...): Target container is not a DOM element.
```

is my fault. In my `app/assets/javascripts/application.js`, I had the line to include the bundle.js file and since this file is brought into the layout in the head section - when the DOM node that react app needs is not ready - it throws an error. We use `bundle.js` as a precompiled asset, so we don't need to bring it in as part of `appication.js`. There's an easy fix in Sprockets for it. If you would like to ignore a file in your directory you use the `stub` call. So, my `application.js` file now looks like:

```
// This is a manifest file that'll be compiled into application.js, which will include all the files
// listed below.
//
// Any JavaScript/Coffee file within this directory, lib/assets/javascripts, vendor/assets/javascripts,
// or any plugin's vendor/assets/javascripts directory can be referenced here using a relative path.
//
// It's not advisable to add code directly here, but if you do, it'll appear at the bottom of the
// compiled file.
//
// Read Sprockets README (https://github.com/rails/sprockets#sprockets-directives) for details
// about supported directives.
//
//= require jquery
//= require jquery_ujs
//= require turbolinks
//= require_tree .
//= stub bundle
```