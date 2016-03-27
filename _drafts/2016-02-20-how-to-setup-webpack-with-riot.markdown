---
layout: post
comments: true
title: "How to setup Webpack with RiotJS"
date: 2016-02-20 09:00:00
categories: general
---
Setting up 

First we install webpack (@1.12.13 at the time of writing) riot and babel:

{% highlight bash %}
npm i -D webpack webpack-dev-server riot babel-core babel-loader babel-preset-es2015
{% endhighlight %}

Next, lets setup the directory structure.
{% highlight bash %}
mkdir -p src src/views dist
{% endhighlight %}

Lets setup a npm script to run the webpack build process.
In ``` package.json ``` add the following:

{% highlight json %}
  "scripts": {
    "build": "./node_modules/.bin/webpack"
  }
{% endhighlight %}

Next we need to create the ``` webpack.config.js ``` file in which we tells Webpack how to build our project.

Create a ``` webpack.config.js ``` file and add the following:

{% highlight javascript %}

module.exports = {
  entry: [
    __dirname + '/src/entry.js'
  ],
  output: {
    path: __dirname + '/dist/',
    filename: 'entry.js'
  },
  devtool: 'eval',
  debug: true,
}

{% endhighlight %}

Lets do a quick test and make sure everything is working.
Make a ``` src/entry.js ``` file and add the following:

{% highlight javascript %}
console.log('It works!')
{% endhighlight %}

Next run the Webpack build:
{% highlight bash %}
npm run build
{% endhighlight %}

Inspect ``` dist/entry.js ```, you should see the Webpack boilerplate code if all worked well. Now is a chance to see how Webpack will handle your code.

Ok lets see our file in the browser. We'll be using the Webpack-dev-server to do that and later enable HMR through it.

In ``` webpack.config.js ``` change ``` entry ```:

{% highlight javascript %}
  entry: [
    'webpack-dev-server/?http://localhost:' + PORT,
    __dirname + '/src/entry.js'
  ]
{% endhighlight %}

The Webpack-dev-server is just small express server that will serve the ``` dist ``` files once they are built.

Let's add a serve script to our ``` package.json ``` file:

{% highlight json %}
  "scripts": {
    "build": "./node_modules/.bin/webpack",
    "serve": "./node_modules/.bin/webpack-dev-server"
  }
{% endhighlight %}

Now, run the serve command:
{% highlight bash %}
npm run serve
{% endhighlight %}
