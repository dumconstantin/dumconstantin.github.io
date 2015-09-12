---
layout: post
title: "Nodejs on Docker"
date: 2015-08-04 09:00:00
categories: devops
---
If you’re trying to use Docker for Nodejs development and would like to have your node modules embed at built time you might discover that it’s not that easy. Trying to install globally or to have them installed in a different location than the one you’re mounting on are either not possible or the overhead might be too big.

What I’ve found is that you could do the following small hack to get them working:

{% highlight html %}
FROM node
WORKDIR /tmp/
ADD package.json package.json
RUN npm install 
VOLUME /app
WORKDIR /app
EXPOSE 8080
CMD rm -rf /app/node_modules && cp /tmp/node_modules /app/ && node start
{% endhighlight %}

Instead of relying on the build process to link the modules to your soon to be app code, you do the join during container startup. Each time you start the container, the node_modules from your app folder will be deleted and replaced with the pre-built ones from the container.

If you need to update the modules in any way just change the package.json and then rebuild your container

{% highlight html %}
docker build -t myapp .
{% endhighlight %}

If you’re starting a project you could add a listener on the package.json and rebuild and start the container automatically each time you change the dependencies. Also it would be a good idea if you could run all npm install modulename from within the container. I recommend you do the following:

{% highlight html %}
docker run -v “$PWD”:/app -p 49000:8080 -d myapp
{% endhighlight %}

and then do

{% highlight html %}
docker exec -ti myapp bash 
{% endhighlight %}

to get a terminal into the container where you can run your commands. 

I feel this way you remove the responsibility from your OS to have the correct version of npm/node or any other dependencies you add to your container to run even simple npm install commands.
