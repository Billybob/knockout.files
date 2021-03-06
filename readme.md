# Knockout.Files

A simple binding for knockout 2.3+ to allow you to load files into the browser, using the HTML5 FileReader functionality.

Now with module loader and drag and drop support... SUCH WOW!

## Installing

Add knockout-2.3.js to your project, then knockout.files.js to your project..

## Example

A simple example of allowing a user to load a file and then callback with the (file, data) arguments:
```
<input type="file" id="some-file-element" data-bind="files: SomeFileLoadedCallback" /> 
<script>
	var SomeFileLoadedCallback = function(file, data) {
		// Do something with file and data
	}
</script>
```

A more complicated example with custom settings:
```
<input id="some-files-element" data-bind="files: { onLoaded: SomeLoadedCallback, onProgress: SomeProgressCallback, OnError: SomeErrorCallback, fileFilter: 'image.*', readAs: 'binary' }" />
```

As shown above you can hook into any of the file loading events and get access to the data to display things like progress bars, and custom file filters, which although the accepts attribute should enforce this for you but does not currently work in all browsers. So in this case you can constrain loaded files and just ignore ones that dont match the pattern. Finally it is loading the data as a binary string in the above example, however this can be converted to use other supported types.

The available options for this binding are:

* **onLoaded** - The main callback for when the file has been loaded, returns file object and file data
* **onProgress** - The progress callback which is fired at intervals while loading, returns file object, amountLoaded and totalAmount
* **onError** - The callback for when things didnt go how you expected...
* **fileFilter** - The regex pattern to match the mime types against, e.g (image.*, application.*|text.*), if a file does not meet the filter it will raise an error
* **maxFileSize** - The maximum file size for loaded files in bytes, if a file exceeds the file size it will raise an error
* **readAs** - to indicate how you want to read the file, options are (text, image, binary, array), the default behaviour is image
* **allowDrop** - to indicate you want to enable drag and drop functionality for files on this element
* **hoverClass** - the class to apply when you are hovering a file over the drag and drop compatible dropzone

The only required argument is the loaded callback, which can be defined as a root argument:

```
<input data-bind="files: callback"/>
or
<input data-bind="files: {onLoaded: callback}"/>
```
Here is an example of what it does and how to use it, but BYOF (Bring Your Own Files).
[View Example](https://rawgithub.com/grofit/knockout.files/master/example.html)