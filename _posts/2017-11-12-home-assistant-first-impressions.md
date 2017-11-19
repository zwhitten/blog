---
layout: post
title: Home-Assistant First Impressions
date: 2017-11-12 16:48:00 -0500
comments: true
tags: home-assistant
---

I had a spare Raspberry Pi 2 laying around, so I decided to give [home-assistant](https://home-assistant.io/) a spin. Overall Home Assistant is very impressive. There are connectors for just about every type of "Smart Home" device you coul possibly want to connect. It has auto-discovery for certain types of devices, but most others require configuration changes to enable. 

### Installation
On my pi 2 the installation was actually a little bit painful (time-wise). They do have a script available that does all of the heavy lifting like creating a separate user account to run home-assistant as, installing the necessary OS dependencies, pulling down the python packages needed, etc. The painful part was likely due to the low power nature of the pi 2, but it took over 4 hours for this process to complete for me. There were many points during the installation where I wasn't sure if it had locked up or if it was still going because there was no progress indication. 

### Hope you like YAML
Most of the configuration Home Assistant supports has to be done through YAML configuration files. I have not gotten too deep into this yet besides enabling Z-Wave and getting a USB Z-Wave receiver and motion sensor connected. 

They're connected but not doing much yet. I didn't find much documentation about how to configure things, but there are links to quite a few Github projects where people have provided example configurations. 

I was also able to connect to the Weather Underground API to pull local weather information for my area. I haven't yet gotten this data grouped into a useful UI component though. 

I'm still going through the example files learning what's possible and how to make it happen. 

### Still TODO
I'm planning to configure more complicated triggers and events based on the few Z-Wave devices I have. I'll post again later to update on my progess so stay tuned!

I'd also like to delve into what configurations are available for grouping sensors and devices on the home screen. 

There are also a number of plugins people have written I'd like to check out. One specifically was a floorplan addon that lets you visualize your house and where various sensors/devices are. [ha-floorplan](https://github.com/pkozul/ha-floorplan)

There are also instructions for setting up Home Assistant as a [hidden Tor service](https://home-assistant.io/docs/ecosystem/tor/) which seems pretty awesome as well. 