---
layout: default
title: "Index"
---

Verto is a WebRTC communication platform based on [FreeSWITCH](https://freeswitch.org/). We divide it in three other projects: mod_verto, verto and verto-communicator. 

## mod_verto

It's the FreeSWITCH module responsible for abstracting SIP protocol. It makes easier to connect through a web socket and make audio and video calls. Its development is bundled with FreeSWITCH core.

## verto

The jQuery library which connects and deals with FreeSWITCH mod_verto through a web socket.

## verto-communicator

[Verto Communicator](https://freeswitch.org/confluence/display/FREESWITCH/Verto+Communicator) is the web application responsible for expose mod_verto features to users. It's based on verto jQuery library and uses AngularJS.
