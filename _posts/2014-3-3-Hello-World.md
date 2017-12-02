---
layout: post
title: Adding Sass to create-react-app
published: true
---
##Introduction

Facebook's [create-react-app](https://github.com/facebookincubator/create-react-app) is a great tool to get you up and running with a React app that you can use as the basis for your own app. However, you'll soon want to add further functionality to this template.
This post describes how to modify the the basic app to use Sass. Note that these instructions are taken from the create-react-app site, so for in-depth instructions head [over there](https://github.com/facebookincubator/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-css-preprocessor-sass-less-etc).

##Install required packages

We'll be using the [node-sass-chokidar](https://github.com/michaelwayman/node-sass-chokidar) command line interface for Sass. Install by running the command:

`npm install node-sass-chokidar --save-dev`

Also, we'll install [npm-run-all](https://github.com/mysticatea/npm-run-all) which allows us to run multiple npm scripts in parallel:

`npm install npm-run-all --save-dev`


##Modify npm scripts

The existing scripts section of the package.json file should look something like this:

```
"scripts": {
		"start": "react-scripts start",
    	"build": "react-scripts build",
    	"test": "react-scripts test --env=jsdom",
    	"eject": "react-scripts eject"
    }
```
Modify it as below:
```
"scripts": {
    "build-css": "node-sass-chokidar src/ -o src/",
    "watch-css": "npm run build-css && node-sass-chokidar src/ -o src --watch --recursive",
    "start-js": "react-scripts start",
    "start": "npm-run-all -p watch-css start-js",
    "build-js": "react-scripts build",
    "build": "npm-run-all build-css build-js",
    "test": "react-scripts test --env=jsdom",
    "eject": "react-scripts eject"
  }
```
To process any .scss files in the src folder to .css, execute `npm run build-css`.
Executing `npm start` will start the server and run node-sass-chokidar in watch mode.

