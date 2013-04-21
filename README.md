Preload.js
========

#### File Preloader API ####
The idea behind the Preload API was to create a simple, easy to use library for preloading files. Multiple event listeners are available and it removes the cumbersome uses of `XMLHttpRequest`, `Blob`, and `FileReader` to make your code easily understandable.

### Usage ###
Download [Preload.js](./Preload.js) and include it in your html.
```html
<script src='js/Preload.js'></script>
```
This code creates a Preload object, loads an audio file through it, and displays it's progress in a loading bar. Once finished it plays the audio file.
```html
<style>
	body{
		margin:0px;
		padding:0px;
	}
	#meter{
		height:20px;
		background:black;
	}
</style>

<audio id='player' src='' controls='true'></audio>
<div id='meter'></div>

<script>

	var loader = new Preload();
	
	loader.onload = function(event){
		document.getElementById('meter').style.width = '100%';
		document.getElementById('player').setAttribute('src',event.response);
		document.getElementById('player').play();
	};
	loader.onprogress = function(event){
		document.getElementById('meter').style.width = event.progress*100+'%';
	};

	loader.open('audioFile.mp3');
	loader.read();

</script>
```
### Constructor ###
Returns a new Preload object.
```Javascript
new Preload()
```

### Methods ###
The `open` command directs the Preload object to it's target url, which cannot be cross-origin unless the external server allows it in its Access-Control-Allow-Origin settings. Note that you may add the extra parameter "text" to receive the file as raw text, otherwise the response will be a dataURL.

The Preload object has four events called during the load: `onload` `onprogress` `onabor` `onreadystatechange`. Note that all four functions have events passed into them containing response data, preload data, and the Preload object. You may also use the `addEventListener` function to set these events.

The `read` command starts loading the url provided in the open command.

The `sample` command grabs all header information for the url provided in the open command.

The `abort` command aborts all current progresses within the Preload object.

### Change Log ###
11 22 2012
* Fixed mobile construction error

11 16 2012
* Added `onerror` event listener
* Correctly escaped the `addEventListener` function
* The response type can now be changed to raw text

11 04 2012
* Added `onabort` event listener
* Fixed cross browser support bug for the `blobConstructor`

11 02 2012
* First alpha release
