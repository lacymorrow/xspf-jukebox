xspf-jukebox
============

# Documentation
***
### Easy Install

##### 1. Copy all of the player files to your server. 
Edit the first line of the `xplay.php` file to point to your media directory:

`$media = "media"`

Edit any options you wish, playlist cacheing is turned on by default.

##### 2. Include the [SWFObject](http://code.google.com/p/swfobject/) javascript code into your page `<head>`:
`<script type="text/javascript" src="http://ajax.googleapis.com/ajax/libs/swfobject/2.2/swfobject.js"></script>`

##### 3. Create a `<div>` to hold your content:
 `<div id="flashcontent">
      <!-- this will be replaced -->
  </div>`
  
##### 4. Invoke the player via javascript:<h5>

    <script>
    var params = {};
    params.wmode="transparent";
    params.allowscriptaccess="always";
    swfobject.embedSWF("xspf_jukebox.swf?playlist_url=xplay.php&skin_url=skins/iTunes[&param1=value&param2=value...]","flashcontent", "skin width", "skin height", "7.0.0", "", {}, params, {});
    </script>

Notice the values highlighted above, you must specify valid file paths for both the `playlist_url` and `skin_url` as well as the skin `width` and `height`. You may also specify any of the optional parameters following the `playlist_url`. For example:

The entire url for the .swf on the demo page is:

    xspf_jukebox.swf?playlist_url=xplay.php&skin_url=skins/iTunes&autoplay=true&alphabetize=true&autoload=true&autoresume=true&main_image=images/artwork.jpg&shuffle=true&statsurl=stats.php

That&rsquo;s it! The XSPF Jukebox is now installed.


##### Single track mode

You can also use the Jukebox to play a single .mp3 or .flv file, using the following two parameters in place of playlist_url:

*   `track_title` : label of track
*   `track_url` : url of track

* * *

##### Optional Parameters

*   `playlist_url` : the url of the xspf file to load
*   `skin_url` : url of the skin folder
*   `loadurl` : url linking to a text file containing all variables. cuts down on html coding and file sizes, one file can be used by many players
*   `activeDownload` : boolean value to allow or disallow direct downloads of tracks, default is false
*   `alphabetize` : boolean value to alphabetize playlist, default is false
*   `autoload` : boolean value that makes the playlist load without the initial user click, default is false
*   `autoplay` : boolean value that makes the playlist load and the music start without the initial user click, default is false
*   `autoresume` : boolean value that allows players on multiple pages to seamlessly continue music as a user browses pages, default is false
*   `buffer` : seconds to preload video before playing, exclude for automatic
*   `crossFade` : either a boolean value, which when true is set to the default time, or the number of seconds to fade (1-12), default is 6 seconds
*   `forceAlphabetize` : boolean value, forces full alphabetizing, including preceding 'the' in artist title, default is false
*   `format` : text to format track label, use "-creator, "-title, "-location, and "-annotation to insert respective values, default is "-creator : -title
*   `gotoany` : boolean value that forces travel to unknown URLs, default is false
*   `image` : url for a jpg image that is shown when autoplay is off
*   `infourl` : global info url for all songs, fills absent playlist info urls
*   `load_message` : message displayed after autoload
*   `main_image` : global image url, fills absent playlist images
*   `mainurl` : right-click &raquo; "about" url
*   `midChar` : character placed to separate creator and title values for tracks, overwritten by format, default is ":
*   `no_continue` : boolean value to turn off automatic song changing, default is false
*   `player_title` : title text, default is "Xspf Jukebox
*   `repeat` : boolean value to set repeat, default is false
*   `repeat_playlist` : boolean value to repeat the playlist, default is true
*   `shuffle` : boolean value to set shuffle, default is false
*   `start_track` : track number for beginning track, default is 1
*   `statsurl` : url to an external script that can collect POST values. Can collect playSong and annotation
*   `timedisplay` : numerical value to show time counter; 0: off, 1: all, 2: elapsed, 3: duration, 4: countdown
*   `trackNumber` : boolean value that adds track numbers to labels, default is false
*   `useId3` : boolean value that forces id3 tag use, default is false
*   `volume_level` : starting volume level percent, default is 100

##### Playlist Format

The XSPF Jukebox uses the [XSPF (&lsquo;spiff&rsquo;)](http://xspf.org) open XML playlist format. A brief example follows:

    <?xml version="1.0" encoding="UTF-8"?>
    <playlist version="0" xmlns="http://xspf.org/ns/0/">
        <trackList>
            <track>
                <location>url of .mp3 audio or .flv video file</location>
                <creator>artist or creator of track</creator>
                <title>title of track</title>
                <annotation>used in place of creator/title if both are absent</annotation>
                <duration>number of milliseconds of track duration</duration>
                <info>url of info link</info>
                <image>url of image, overwrites main_image parameter</image>
                <purchase>url of purchase link</purchase>
            </track>
        </trackList>
    </playlist>

###### NOTE: only `<location>` is required

##### Javascript API

A javascript interface has been added into the player to allow for extended control over the Jukebox. This feature only applies to the Flash 8 version.
Available functions are:

*   `playTrack()` : play/pause the track
*   `stopTrack()` : stop the track
*   `nextTrack()` : advance to the next track
*   `prevTrack()` : go back to the previous track
*   `shuffleToggle()` : turn shuffle on/off
*   `repeatToggle()` : turn repeat on/off
*   `gotoTrack(track number)` : play a specified track
*   `addTrack(track id, location, title, creator, info url, purchase url, image, annotation)` : add a track to the playlist

To control the Jukebox using Javascript, make sure that you have an id set in the object and embed tags for the embed script. To call a function, use the format: 

`window.document.xspfJukebox.playTrack();`

For example:

`<a href="javascript:window.document.xspfJukebox.playTrack();">Click to Play </a>`

* * *

# Skin Documentation

The XSPF Jukebox uses a custom XML format to specify the player appearance. The skin.xml files are in the following format:

    <?xml version="1.0" encoding="UTF-8"?>
    <skin version="0" xmlns="http://xsml.org/ns/0/">
        <name>skin name</name>
        <width>skin width</width>
        <height>skin height</height>
        <author>skin author</author>
        <email>author?s email</email>
        <website>author?s website</website>
        <comment>author?s comments</comment>
        <object>
               all skin objects reside between the <object> tags
        </object>
    </skin>

##### Skin Objects

*   `<background x="" y="" width="" height="" scale="" image="" shape="" border="" color="" borderColor="" alpha="" />`
*   `<image x="" y="" z="" width="" height="" image="" alpha="" url="" target="" hoverMessage="" />`
*   `<shape x="" y="" z="" width="" height="" shape="" border="" color="" borderColor="" alpha="" url="" target="" hoverMessage="" />`
*   `<text x="" y="" z="" size="" color="" font="" text="" border="" bold="" italic="" underline="" alpha="" url="" target="" hoverMessage="" />`
*   `<playlist x="" y="" z="" width="" height="" size="" color="" font="" selectedColor="" bold="" italic="" underline="" alpha="" hoverMessage="" />`
*   `<badge x="" y="" width="" height="" />`

##### Function Objects

All function objects begin with an <object> tag, and are distinguished through a `label` attribute. Most labels have similar attributes, but there are some slight differences.

*   `<object label="playButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="playpauseButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="stopButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="prevButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="fwdButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="shuffleButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="repeatButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="scrollButton" x="" y="" z="" width="" height="" scale="" image="" color="" bgColor="" alpha="" bgAlpha="" hoverMessage="" />`
*   `<object label="scrollupButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="scrolldownButton" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="startButton" x="" y="" z="" width="" height="" scale="" color="" alpha="" hoverMessage="" />`
*   `<object label="infoButton" x="" y="" z="" size="" color="" font="" text="" bold="" italic="" underline="" target="" hoverMessage="" />`
*   `<object label="purchaseButton" x="" y="" z="" size="" color="" font="" text="" bold="" italic="" underline="" target="" hoverMessage="" />`
*   `<object label="downloadButton" x="" y="" z="" size="" color="" font="" text="" bold="" italic="" underline="" target="" hoverMessage="" />`
*   `<object label="playDisplay" x="" y="" z="" width="" height="" scale="" color="" alpha="" hoverMessage="" />`
*   `<object label="imageDisplay" x="" y="" z="" width="" height="" scale="" color="" alpha="" hoverMessage="" />`
*   `<object label="videoDisplay" x="" y="" z="" width="" height="" scale="" alpha="" hoverMessage="" />`
*   `<object label="trackDisplay" x="" y="" z="" width="" size="" color="" font="" text="" align="" bold="" italic="" underline="" hoverMessage="" />`
*   `<object label="timeDisplay" x="" y="" z="" size="" color="" font="" text="" bold="" italic="" underline="" hoverMessage="" />`
*   `<object label="fulltimeDisplay" x="" y="" z="" size="" color="" font="" text="" bold="" italic="" underline="" hoverMessage="" />`
*   `<object label="volumeDisplay" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="timeBar" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`
*   `<object label="loadBar" x="" y="" z="" width="" height="" scale="" image="" color="" alpha="" hoverMessage="" />`

##### Labels

*   `playButton` : a play button, toggles between play and pause
*   `playpauseButton` : a static play pause button, toggles between play and pause
*   `stopButton` : a stop button, stops the track
*   `prevButton` : a previous button, changes to the previous track
*   `fwdButton` : a forward button, changes to the next track
*   `shuffleButton` : a shuffle button, toggles on/off
*   `repeatButton` : a repeat button, toggles on/off
*   `scrollButton` : a scroll button with background, scrolls playlist
*   `scrollupButton` : an up arrow, scrolls playlist up
*   `scrolldownButton` : a down arrow, scrolls playlist down
*   `startButton` : a rectangle to indicate click location to start load or play, set alpha to 0
*   `infoButton` : text button to follow the current info link in a playlist
*   `purchaseButton` : text button to follow the current purchase link in a playlist
*   `downloadButton` : text button to directly link to the currently playing mp3
*   `playDisplay` : displays current track images
*   `imageDisplay` : displays current track images
*   `videoDisplay` : displays video tracks
*   `trackDisplay` : displays currently playing track
*   `timeDisplay` : displays current track time in a standard format ?00:00?, toggles between time, duration, and time remaining
*   `fulltimeDisplay` : displays current track time in a full format ?00:00/00:00?, displays time and duration
*   `volumeDisplay` : displays a volume bar to change track volume
*   `timeBar` : displays current track percentage in bar form, click to scan track
*   `loadBar` : displays loaded percentage for the current track in bar form

##### Attributes

*   `x` : number : the x value or percentage for placing an object
*   `y` : number : the y value or percentage for placing an object
*   `z` : number : the z value, or depth of an object.
*   `width` : number : the width of an object
*   `height` : number : the height of an object
*   `scale` : number : used in place of width/height. scales the object while retaining default aspect ratio. 1 equals no scale
*   `size` : number : font size. size must be preceded by a + for infoButton, purchaseButton, and downloadButton. ex: +15
*   `image` : url : load an image in place of the default symbol
*   `shape` : rectangle/rectRounded/circle/triangle : draws a shape for an object
*   `border` : number : defines a shape?s border width
*   `color` : hex code : sets the color of an object. ex: ff0088
*   `borderColor` : hex code : sets the color of an shape?s border
*   `bgColor` : hex code : sets the color of an object?s background
*   `selectedColor` : hex code : sets the color of the current track in the playlist
*   `font` : font name : sets the text font
*   `text` : text : displayed text
*   `align` : left/center/right : used only for trackDisplay. aligns text
*   `bold` : boolean : sets text bolding on/off
*   `italic` : boolean : sets text italics on/off
*   `underline` : boolean : sets text underline on/off
*   `alpha` : percent : sets alpha channel of object
*   `bgAlpha` : percent : sets alpha channel of an object?s background
*   `url` : url : allows an object to link to a web page
*   `hoverMessage` : text : message displayed on mouse over