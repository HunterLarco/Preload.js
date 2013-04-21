'''(title)Preload.js

'''(sub)File Preloader API
'''(paragraph)The idea behind the Preload API was to create a simple, easy to use library for preloading files. Multiple event listeners are available and it removes the cumbersome uses of XMLHttpRequest, Blob, and FileReader to make your code easily understandable.
'''(paragraph)Note: see [FileHandler.js](./FileHandler.md) for more file handlers and functions including the Preload API.

'''(sub)Usage
'''(paragraph)Download [Preload.js](./Preload.js) and include it in your html.
'''(code:html)<script src='js/Preload.js'></script>
'''(paragraph)This code creates a Preload object, loads an audio file through it, and displays it's progress in a loading bar. Once finished it plays the audio file.
'''(code:html)<style>
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

'''(sub)Constructor
'''(paragraph)Returns a new Preload object.
'''(code:javascript)new Preload()

'''(sub)Methods
'''(paragraph)The {func~open} command directs the Preload object to it's target url, which cannot be cross-origin unless the external server allows it in its Access-Control-Allow-Origin settings. Note that you may add the extra parameter "text" to receive the file as raw text, otherwise the response will be a dataURL.
'''(paragraph)The Preload object has four events called during the load: {func~onload} {func~onprogress} {func~onabort} {func~onreadystatechange}. Note that all four functions have events passed into them containing response data, preload data, and the Preload object. You may also use the {func~addEventListener} function to set these events.
'''(paragraph)The {func~read} command starts loading the url provided in the open command.
'''(paragraph)The {func~sample} command grabs all header information for the url provided in the open command.
'''(paragraph)The {func~abort} command aborts all current progresses within the Preload object.

'''(sub)Change Log
'''(paragraph)11/22/2012
'''(bullet)Fixed mobile construction error
'''(paragraph)11/16/2012
'''(bullet)Added {func~onerror} event listener
'''(bullet)Correctly escaped the {func~addEventListener} function
'''(bullet)The response type can now be changed to raw text
'''(paragraph)11/04/2012
'''(bullet)Added {func~onabort} event listener
'''(bullet)Fixed cross browser support bug for the {func~blobConstructor}
'''(paragraph)11/02/2012
'''(bullet)First alpha release