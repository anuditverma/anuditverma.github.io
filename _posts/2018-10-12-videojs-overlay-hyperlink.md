---
layout: post
title: videojs-overlay-hyperlink
tags: [videojs, videojs-plugin, video]
---


A simple video.js plugin to display hyperlinks during video playback using overlays. This plugin is built upon popular video.js plugin called videojs-overlay.<br>

## Static Preview

<center><img src="/assets/img/videojs-hyperlink-screenshot.jpg"></center>

### Live Demo: [Link](https://rawgit.com/anuditverma/videojs-overlay-hyperlink/master/index.html)

## Download
Click [here](https://github.com/anuditverma/videojs-overlay-hyperlink/releases) to download __videojs-overlay-hyperlink__ or `git clone` it into your production directory.

```ssh
git clone https://github.com/anuditverma/videojs-overlay-hyperlink.git
```

## Getting Started

First of all, import the plugin's javascript and css files into your webpage.
```html
<!-- js -->
<script src="path/to/js/video.js"></script>
<script src="path/to/js/videojs-overlay-hyperlink.js"></script>

<!-- css -->
<link href="path/to/css/video-js.css" rel="stylesheet">
<link href="path/to/videojs-overlay-hyperlink.css" rel="stylesheet">
```

After importing, your HTML document should look something like [this](https://github.com/anuditverma/videojs-overlay-hyperlink/blob/master/index.html).

## Define Hyperlink

Add another javascript to define your target hyperlink, just assign `yourLink` variable with your preferred value. 

```js
<script type='text/javascript'>
  var yourLink = "https://www.google.com/search?q=documentaries+on+oceans";
</script>
```
## Configure Setup

The main section of your setup, where you can configure the positioning and duration of the hyperlink.

```js
<script>
    (function(window, videojs) {
        var player = window.player = videojs('videojs-overlay-player');
        player.overlay({
            content: '<a href=# onclick="location.href=yourLink;return false;">Checkout More Documentaries on Oceans</a>',
            debug: true,
            overlays: [{
                start: 0,
                end: 15,
                align: 'bottom-left'
            }, {
                start: 15,
                end: 30,
                align: 'bottom'
            }, {
                start: 30,
                end: 45,
                align: 'bottom-right'
            }]
        });
    }(window, window.videojs));
</script>
```
### Meaning of the plugin options:

#### `content`

__Type:__ `String`, `Element`, `DocumentFragment`
__Default:__ `"This overlay will show up while the video is playing"`

_This setting can be overridden by being set on individual overlay objects._

The default HTML that the overlay includes.

#### `overlays`

__Type:__ `Array`
__Default:__ an array with a single example overlay

An array of overlay objects. Here you can define your hyperlink name, and this overlay object should consist of:

- `start` (`String` or `Number`): When to show the overlay. If its value is a string, it is understood as the name of an event. If it is a number (in seconds), the overlay will be shown when that moment in the playback timeline is passed.
- `end` (`String` or `Number`): When to hide the overlay. The values of this property have the same semantics as `start`.

#### `align`

__Type:__ `String`
__Default:__ `"top-left"`

_This setting can be overridden by being set on individual overlay objects._

Where to display overlays, by default. Assuming the included stylesheet is used, the following values are supported: `"top-left"`, `"top"`, `"top-right"`, `"right"`, `"bottom-right"`, `"bottom"`, `"bottom-left"`, `"left"`.


## See also:
- Highly customizable video player framework, [video.js](http://videojs.com/).
- Similar video.js [plugins and skins](http://videojs.com/plugins/).

Thank you for reading.