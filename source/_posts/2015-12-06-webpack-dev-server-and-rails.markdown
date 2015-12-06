---
layout: post
title: Webpack dev server and Rails
date_string: 06 November 2015
--- 

[Webpack dev server](https://webpack.github.io/docs/webpack-dev-server.html) is pretty awesome. In my [last post](http://ploughthroughruby.co.uk/2015/11/30/integrate-react-es6-webpack-babel-with-rails.html/), I set up React, ES6, Babel and Webpack and the only thing outstanding was the webpack dev server. 

With a webpack dev server running, developers can update their code and have the code changes show up straightaway in the browser, thanks to websockets. In order to implement it for a rails application, I did the following:

```
<% if Rails.env.development? %>
  <%= javascript_include_tag 'http://localhost:9999/bundle.js', 'data-turbolinks-track' => true %>
<% else %>
  <%= javascript_include_tag 'bundle', 'data-turbolinks-track' => true %>
<% end %>
```

For development mode, I am downloading the `bundle.js` from `localhost:9999`. That's the port where the webpack dev server is running at. For the production mode, the `bundle.js` is being read from the `app/assets/javascripts' directory. 

I have the following in my `package.json` to to run the webpack dev server on port 9999:

```
{
  "name": "ecommerce-checklist",
  "version": "0.0.1",
  "description": "Ecommerce checklist",
  "scripts": {
    "start": "webpack-dev-server --content-base ../app/assets/javascripts --port 9999",
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

Note the bit under `scripts -> start`. 

This completes the react and webapck setup for a rails application. 

One thing to bear in mind, is to create a production ready bundle.js before deploying this application, but that can be part of a capistrano deployment hook.