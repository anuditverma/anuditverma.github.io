---
layout: post
title: Make Your Own Wireless Music Streamer with Raspberry Pi
tags: [DIY, music, raspberry pi]
thumbnail-img: https://www.anudit.in/assets/img/wifi_streamer/rPi.jpg
share-img: https://www.anudit.in/assets/img/wifi_streamer/rPi.jpg
---

Yes! You read it right. DIY your wireless music streamer. And this is not a conventional Bluetooth-based wireless player we use over A2DP for your Bluetooth-enabled speakers. It is even better. __With the help of a Raspberry Pi, you can make just any speaker with a 3.5 mm audio connector to receive high-fidelity music from your Android, iPhone, Mac or PC.__

The main advantage of such a setup is that you can stream music to your stereo setup from any part of your home. Even beyond the range of Bluetooth. Sounds cool (pun intended), right?

So let’s dive into this tutorial and leverage the hardware of your awesome Raspberry Pi. Here are the things we will need to move forward:

<h3>Requirements:</h3>
<h4>Hardware:</h4>

* Raspberry Pi (Model 2, Model 3, Model 400; A or B variants)
* Mouse and Keyboard to Input on your Pi.
* Monitor for Display (required once for executing the scripts)
* Ethernet Cable or in-built Wi-Fi Adapter (for connecting to local Wi-Fi router)

<h4>Software:</h4> 

* Raspbian, Ubuntu (MATE, Snappy), Debian, most Linux based OS
* git
* [GMediaRender](http://gmrender.nongnu.org/) (a UPnP™ media renderer)
* Some dependencies (we will cover them during installation steps)

NOTE: __Please make sure that your Raspberry Pi and your playback devices (phone or laptop) are on the same network.__

<h3>Installation:</h3>
Follow these steps to install and setup the streamer:

1: Tools for bootstrapping the compilation configuration.

```bash
sudo apt-get install autoconf automake libtool pkg-config
```
2: Libraries for gmrender (gstreamer).

```bash
sudo apt-get update
sudo aptitude install libupnp-dev libgstreamer1.0-dev \
             gstreamer1.0-plugins-base gstreamer1.0-plugins-good \
             gstreamer1.0-plugins-bad gstreamer1.0-plugins-ugly \
             gstreamer1.0-libav
```
3: Choose the Sound Server (Pulse or ALSA). Use Pulse for better quality. See the differences [here.](https://ubuntuforums.org/showthread.php?t=1794581)

```bash
sudo aptitude install gstreamer1.0-pulseaudio
```
__OR__

```bash
sudo aptitude install gstreamer1.0-alsa
```
<br>
<h3>Build & Customisation</h3>
Now let us build our renderer.

1: Check out the source.

```bash
git clone https://github.com/hzeller/gmrender-resurrect.git
```

2: Configure & build.

```bash
cd gmrender-resurrect
./autogen.sh
./configure
make
```

3: Now run gmrender directly from here if you want. The -f option provides the name under which the UPnP renderer advertises.

```bash
./src/gmediarender -f "My Renderer"
```

 Then it will be ready for renderering, as shown below. 
![Raspbian Setup](/assets/img/wifi_streamer/raspbian.jpg "Terminal on Raspbian")

You can name your renderer anything you want based on the location of the sound system (for example Living Room, Hall). Or you can name it after your speakers. I gave the Gravity Speakers.

4: Make Final Binary. 

```bash
sudo make install
```
The final binary is in ```/usr/local/bin/gmediarender``` (unless you changed the PREFIX in the configure step).


<h3>Let's Play Some Music</h3>
Connect your sound system/speakers to your Raspberry Pi through an onboard 3.5 mm audio connector, a normal 3.5 mm to RCA Audio cable would be sufficient for this setup.

Now you will need a UPnP™ controller/client to send some playable content to your Raspberry Pi, I am using [BubbleUPnP](https://play.google.com/store/apps/details?id=com.bubblesoft.android.bubbleupnp) and you can use any of the UPnP™ client/stream-able Apps.

* Open BubbleUPnP App.
* Click on the overflow button in the top left corner.
* Look for a 'Local Renderer', your local renderer will appear under the local renderers' list, if you are unable to see it, check your phone if it is connected to the WiFi network or not, __your local renderer and your phone should be on the same network to communicate with each other.__
* Select your Local Renderer, now go to Library and select your favourite track you want to play, you can also create a playlist and play all your tracks that are stored locally on your phone. (This is one of the advantages that BubbleUPnP offers over other Apps.)

![BubbleUPnP](/assets/img/wifi_streamer/bubble_upnp.jpg "BubbleUPnP App")

<h3>Also on Windows...</h3>
Because yeah, fortunately, there is an inbuilt support for streaming UPnP™/DLNA content right from Windows Media Player, so kudos to Microsoft for this. Follow these steps for streaming your content.

* Open Windows Media Player.
* Select your favourite track, in the right side panel, there will be a 'Play To' icon on the Play Tab.
* Select this option and wait for your local renderer to appear.

<center>OR</center>

* Quickly right-click on the audio file you want to play/stream.
* On the context menu observe the 'Cast Device' sub-menu.
* Select your local renderer again and Voila! 

Now you should be able to listen to your songs streamed over WiFi to your sound system setup. You can add your tracks in this small player Window and create your own digital mixtape.

<center><img src="/assets/img/wifi_streamer/win_playto.jpg" alt="Windows Media Player"></center>

I hope you enjoyed setup-ing your own wireless music streamer. Also, one more thing you can add this streaming service to the startup boot sequence. This would help in not needing to connect to a display every time to manually execute the command to run this service. Special thanks to [Henner Zeller](https://github.com/hzeller) for making a resurrected version of the old [GMediaRender](http://gmrender.nongnu.org/) project and adding useful features. I will leave you with some useful links to make your music-listening experience even more enjoyable.

<h3>Useful Links:</h3>

* The list of compatible stream-able apps/options/features of various platforms (Linux, Android, Windows, iOS, macOS, iPadOS) is present [here.](https://github.com/hzeller/gmrender-resurrect/wiki/Comptibility)
* And the list of UPnP/DLNA controllers tested with gmrender-resurrect is present [here.](https://github.com/hzeller/gmrender-resurrect/wiki/Compatibility)
* If you want to add a small LCD display to view songs' info like track name, artist's info, album etc then make sure to check out this [repository.](https://github.com/hzeller/upnp-display)

Thank you for reading.