# A Quick Guide to Chrome Apps using Creationix Module Loader

## Introduction

This is a quick guide to using the nice [module loader that creationix has created](https://github.com/creationix/chrome-app-module-loader) to allow loading modules with the same style as in Nodejs. 

## Trying it out

For the impatient:
* clone this git repo
* npm install in the cloned folder
* in chrome goto chrome://extensions, tick "Developer mode"
* still in extensions page, press the "Load unpacked extension..." button and select the folder you cloned the git repo into
* You should see the "Git" extension appear in the list of extensions on the page, then just click Launch link under the Git 
extension entry.

### How it works

### Chrome App Manifest

Chrome apps need a [manifest.json](manifest.json) where they declare the permissions they require as well as other metadata about the app.

The keypoints of the example included in this gist are:
* the background scripts array defines the scripts that will be run when the app is running
* the socket permission gives the app use of the raw tcp sockets api (*no* x-origin security policy applies!)

__Note:__ in this simple case, all the background script does is add a listener for the app being launched that will then open a new window with [index.html](index.html)


### Using the Module Loader

Finally the crux of this guide, the index.html page makes use of the loader to load the dependencies of the main js code and the loader will also recurse through and load the dependencies of the dependencies etc.

The single html <script> elem points to the location of the module loader js and uses the ```autorequire``` attribute to point to the
main (aka index.js) of the top-level code module you are using.

In this case its [ls-demo.js](ls-demo.js) which then has the normal requires you would use in Nodejs.

For this demo, I declared all the dependencies in package.json, __including the loader module itself__ and used npm to install them all in node_modules folder.







