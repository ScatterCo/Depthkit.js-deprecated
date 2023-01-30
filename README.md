# Depthkit.js
[![Build Status](https://travis-ci.org/juniorxsound/DepthKit.js.svg?branch=master)](https://travis-ci.org/juniorxsound/DepthKit.js)                [![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)

A plugin for visualising [Depthkit](http://www.depthkit.tv/) volumteric captures using [Three.js](https://github.com/mrdoob/three.js) in WebGL. The plugin requires Three.js and a Depthkit *combined-per-pixel* video export.

![Depthkit.js screencapture](https://raw.githubusercontent.com/ScatterCo/DepthKit.js/master/assets/gh/banner.gif)

## Getting started:
1. Fork/Clone/Download
1. Open Git Bash in the root directory.
1. Run ```npm install``` to install all dependcies.
1. Run ```npm run start``` to start an http server.
1. To confirm that the http server is running, open a browser, and go to ```localhost:8080```. If the server is running, you should see a list view of the files and folders in your directory.
1. To see an example, navigate the browser to ```http://localhost:8080/examples/simple.html```.
1. To load your own Depthkit clip, move your Depthkit combined-per-pixel video and metadata into the /assets bin. In ```simple.html```, find the ```depthkit.load()``` call on line 98, and replace the TXT and MP4 references with the location and filename of your own asset. Save the page and refresh.

Include ```depthkit.js``` or ```depthkit.min.js``` after loading ```three.js``` in your project.

### Creating a character
```JavaScript
var depthkit = new Depthkit();
depthkit.load(
	"myClip.txt",
	"myClip.mp4",
	character => {
		scene.add(character);
	}
);
```
Where the first and second arguments are the path to the metadata file and the *combined-per-pixel* video exported by Depthkit.
The third argument is a callback that is passed a THREE.Object3D object representing the Depthkit character.

### Controlling a character
Calling ```new DepthKit()``` returns an object that has the neccesery methods to control the playback and rendering of the character

```depthkit.play()``` - Play the video

```depthkit.pause()``` - Pause the video

```depthkit.stop()``` - Stop and rewind to begining

```depthkit.setLoop(isLooping)``` - Set loop to true or false

```depthkit.setVolume(volume)``` - Change the volume of the audio

```depthkit.setOpacity(opacity)``` - Change opacity

```depthkit.dispose()```
- Dispose and clean the character instance

## Examples:
[Simple Depthkit example](https://juniorxsound.github.io/DepthKit.js/examples/simple.html)

## How to contribute:
1. Fork/Clone/Download
1. Install all dependcies using ```npm install```
1. Use the following node commands:

```npm run start``` uses ```concurrently``` to start an ```http-server``` and to run ```watchify``` and bundle on every change to ```build/depthkit.js```

```npm run build``` to bundle and minify to ```build/depthkit.min.js```

## Credits
The Depthkit.js plugin was developed for [Tzina: A Symphony of Longing](https://tzina.space) and ported with permission from Scatter's Unity Depthkit Plugin.

## Workaround for metadata files from Depthkit 0.5.4 and later
Recently, Depthkit has been updated to support multiple perspectives (Depthkit Studio), slightly altering the structure of assets exported out of Depthkit, and breaking compatibility with Depthkit.js.

Single-perspective Depthkit assets from Depthkit Core and Depthkit Cinema can be modified to the older structure to make them compatible with Depthkit.js using the following steps:

* Locate the metadata file of your Depthkit asset, make a backup of it, and open it in a text/code editor. Editors like SublimeText and Atom can make it easier to read the metadata’s JSON format.
* Locate the ```"numAngles"``` and ```"perspectives"``` objects.
    * Delete the entire ```"numAngles": 1```, line.
    * Within the ```"perspectives"``` array in brackets ```[]```, you’ll find an unnamed object in curly braces ```{}```. 
    * Delete the ```"perspectives" [ {``` preceding the contents of the object, and the ```} ]``` following it. 
    * The remaining contents, beginning with ```"clipEpsilon"``` and ```"crop"``` objects, and ending with the ```"farClip"``` and ```"nearClip"``` and their values, are now elevated to the same level as the other objects in the metadata.
     * Make sure that each object is followed by a comma except for the final one.
* Save this modified version.

## Thanks

Originally written by [@mrdoob](https://github.com/mrdoob) and [@obviousjim](https://github.com/obviousjim) ported and modified by [@juniorxsound](https://github.com/juniorxsound) and [@avnerus](https://github.com/Avnerus). Special thank you to [Shirin Anlen](https://www.shirin.works/) and all the Tzina crew, [@ZEEEVE](https://github.com/zivschneider), [@jhclaura](https://github.com/jhclaura)
