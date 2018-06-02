---
layout: post
title: Creating a Flutter Demo App
date: 2018-06-02 14:15:00 -0500
comments: true
tags: flutter iOS android
---

I've been experimenting lately with [Flutter](https://flutter.io) for building cross platform mobile applications, and I have to say so far I'm pretty impressed.

 I had previously looked into React Native and Nativescript options. Both were/are great especially if you're already a JavaScript developer (or want to be one). React Native is obviously more suited for developers who already have some familiarity with React. Nativescript likewise offers a pretty seamless transition for people already familiar with Angular. The most impressie thing about Nativescript to me was Expo which allows for loading your code onto an actual device without connecting to the computer. 

 ### Enter Flutter...

Flutter offers pretty much all of the same advantages of it's javascript counterparts. Namely, true write once and run anywhere code. One big difference however is that Flutter doesn't interact directly with native components. Flutter animates and draws all of it's components separately which means that there is no JavaScript to native bridge required within the applications. 

Flutter comes with dozens of components out of the box. It's hotreload functionality allows for near instantaneous testing and debugging in the local simulators. Flutter uses the Dart programming language which could be a turn off to some, but I actually found it pretty easy to pick up. There were only a couple of instances where I had to consult the documentation to check the syntax. 

As a test of the framework I created a simple "todo" list style application to track books that I have in my stack to be read. The application has multiple tab views with Lists of items which can be reordered, completed and/or deleted. It's also backed by sqlite using a dart library. In a future post I'll try to dive into the actual implementation of the test application.

All in all the process was super easy, and I had a fully functional "production" ready application in a fraction of the time it would have taken to implement in pretty much any of the other frameworks I have tried. 

Feel free to check out the results on github: 
[Media Queue - Flutter Application](https://github.com/zwhitten/media_queue)