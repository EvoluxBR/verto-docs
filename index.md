---
layout: default
title: "Index"
---

## What's Verto

Verto is a WebRTC communication platform based on [FreeSWITCH](https://freeswitch.org/). We divide it in three other projects: mod_verto, verto and verto-communicator. 


## Verto projects

### mod_verto

It's the FreeSWITCH module responsible for abstracting SIP protocol. It makes easier to connect through a web socket and make audio and video calls. Its development is bundled with FreeSWITCH core.

### verto

The jQuery library which connects and deals with FreeSWITCH mod_verto through a web socket.

### verto-communicator

[Verto Communicator](https://freeswitch.org/confluence/display/FREESWITCH/Verto+Communicator) is the web application responsible for expose mod_verto features to users. It's based on verto jQuery library and uses AngularJS.

## What will be covered

In this tutorial, we're going to learn by examples how to install, import and use verto jQuery library to create a basic video conference web application.

- [getting started]({{ site.baseurl }}/tut/getting-started.html)
- [installing verto]({{ site.baseurl }}/tut/installing-verto.html)
- [importing and initializing verto]({{ site.baseurl }}/tut/initializing-verto.html)
- [making an audio call]({{ site.baseurl }}/tut/making-a-call.html)
- [hanging up a call]({{ site.baseurl }}/tut/hanging-up-a-call.html)
- [answerign a call]({{ site.baseurl }}/tut/answering-a-call.html)
- [adding video support]({{ site.baseurl }}/tut/adding-video-support.html)
- [recovering a call]({{ site.baseurl }}/tut/recovering-a-call.html)

[Click here and get started]({{ site.baseurl }}/tut/getting-started.html).
