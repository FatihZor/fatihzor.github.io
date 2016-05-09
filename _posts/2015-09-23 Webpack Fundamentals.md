---
layout: post
title:  "Webpack Fundamentals"
date:   2015-09-23 22:22:15
categories:  [Javascript]
tags:  [Javascript]
---

WebPack use NPM Not Bower
Use a Module System

WebPack
Command Line Interface
Config Files
Dev Server
Loaders
Production Builds

method1:webpack ./app.js bundle.js

method:2:

webpack.config.js

module.exports = {
   entry:"./app.js",
   output:{
   	  filename:"bundle.js"
   },
   watch:true,
   module:{
   preLoaders:[{
   			test:/\.js$/,
   			exclude:/node_modules/,
   			loader:"bable-loader"
   }],
   	loaders:[
   		{
   			test:/\.es6$/,
   			exclude:/node_modules/,
   			loader:"bable-loader"
   		}
   	]
   },
   
   resolve:{
   		extension:['','.js','.es6']
   	
   }
   

}

webpack

npm install webpack-dve-server -g

command:web-dev-server
localhost:8080/web-dev-server

without the status bar:
webpack-dev-server --inline

commonJs file:

require('./login.js');

module.exports = {
   entry:["./utils","./util"],
   output:{
   	  filename:"bundle.js"
   },
   watch:true
}

Loaders:

bable-core,bable-loader

package.json file scripts section:

”scripts“:{
	“start”:"webpack-dev-server"
}

npm start

webpack -p :will minimize the js file.

webpack-production.config.js:

var devCofig= require('/webpack.config.js');
module.export = devConfig;
var stripLoader = {
	test:[/\.js$/,/\.es6$/],
	exclude:/node_modles/,
	loader:WebpackStrip.loader('console.log')
}

devConfig.module.loaders.push(stripLoader);
module.exports = devConfig;

webpack -- config webpack-production.config.js -p

npm install http-server -g 
http-server

Orgnize the file and folders:


var path = require('path');
module.exports = {
	context: path.resolve('js');
	entry:['./utils','./app.js'],
	output:{
		path:path.resolve('build/js/'),
		publicPath:'/public/assets/js/',
		fileName:'bundle.js'
	},
	devServer:{
		contentBase:'public'
	},
	
	...
}


webpack -d 
debugger;

css Loader
npm install css-loader style-loader
npm install extract-text-webpack-plugin
npm install auto-prefixer-loader
npm install url-loader
npm install file-loader




