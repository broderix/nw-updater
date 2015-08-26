node-webkit updater module
=======================================================

Automatically (and silently) updates node-webkit apps on the background

## How it works?

This code will contact the update API endpoint and if a new version is available, will download and install it.

    var gui = require('nw.gui');
    var currentVersion = gui.App.manifest.version

    var updater = require('nw-updater')({
        'channel':'beta',
        'currentVersion': currentVersion,
        'endpoint': 'http://torrentv.github.io/update.json',
        'pubkey': '-----BEGIN RSA PUBLIC KEY-----\nMII...'
    })

    updater.update() //or updater.check()

    updater.on("download", function(version){
        console.log("OH YEAH! going to download version "+version)
    })

    updater.on("installed", function(){
        console.log("SUCCCESSFULLY installed, please restart")
    })

For an example update.json please visit: [http://torrentv.github.io/update.json](http://torrentv.github.io/update.json)

### Parameters

    var parameters = {
         'channel': boolean,
         'currentVersion': string,
         'endpoint': string,
         'pubkey': string,
         'windowsExeUpdate': boolean,
         'outputDir': boolean|string,
         'downloadToTmpDir': boolean
     };
    var updater = require('nw-updater')(parameter);
    
#### channel

Not used, not implemented yet. Any name for your version (like branch). 

#### currentVersion

Any string matched with pattern '+d\.+d\.+d'. For example, '0.2.5', '1.1.109', etc

#### endpoint

Any url to download update.json file. For an example update.json please visit: [http://torrentv.github.io/update.json](http://torrentv.github.io/update.json)

#### pubkey

Public RSA key, EOL replace with '\n'.

    $ npm install node-sign-release -g
    $ node-sign-release package.nw

Will be generate automatically keypair.json with private and public keys. 

#### windowsExeUpdate

If you need to update not package.nw file. For example you need to update nw.js engine, then you need to update the whole app. 
E.g. windows: prepare setup.exe, zip it to package.nw, configure update.json, upload files to update-server, after updater.on('installed', ..) fired, run as "spawn('.../setup.exe', ...)", exit app. 

#### downloadToTmpDir

Folder to download package.nw file mentioned in update.json. In case if app folder is read-only (windows).

#### outputDir

Folder to extract package.nw. If you use 'windowsExeUpdate: true' param, and app folder is read-only (windows).


## Installation 

With [npm](http://npmjs.org):

[![NPM](https://nodei.co/npm/nw-updater.png?downloads=true)](https://nodei.co/npm/nw-updater/)

## Executable creation

It is designed to work with builds generated with [grunt-node-webkit-builder-for-nw-updater](https://github.com/guerrerocarlos/grunt-node-webkit-builder-for-nw-updater) 

[![NPM](https://nodei.co/npm/grunt-node-webkit-builder-for-nw-updater.png?downloads=true)](https://nodei.co/npm/grunt-node-webkit-builder-for-nw-updater/)

## Update.json:

update.json checksums and signatures can be created using [node-sign-release](http://npmjs.org/package/node-sign-release)

## Kudos

Kudos for the original authors of this module, the [PopcornTime.io](http://popcorntime.io/) developers.
