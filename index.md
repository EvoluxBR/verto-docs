---
layout: default
title: "Index"
---

## What's Verto

Verto is a [FreeSWITCH](https://freeswitch.org/) endpoint that implements a subset of a JSON-RPC connection designed for use over secure web sockets. The initial target is WebRTC to simplify coding and implementing calls from web browsers and devices to FreeSWITCH. This allows a web browser or other WebRTC client to originate a call using Verto into a FreeSWITCH installation and then out to the PSTN using SIP, SS7, or other supported protocol. This moves FreeSWITCH farther out onto the cutting edge of real-time communications technology while maintaining interoperability with SIP and other legacy protocols.

In short words, Verto simplifies communications between modern devices.

### mod_verto

mod_verto is the signaling protocol. It's the FreeSWITCH module responsible for abstracting SIP protocol and it depends on mod_rtc for secure media streaming services. Read more about it on [FreeSWITCH Confluence](https://freeswitch.org/confluence/display/FREESWITCH/mod_verto).

### verto library

The jQuery library which connects and deals with FreeSWITCH mod_verto through a web socket.

## Implemented applications

These are some examples of web clients that can be implemented on top of mod_verto.

- [Original Verto Demo](https://cantina.freeswitch.org/verto/).

- [Verto Communicator](https://cantina.freeswitch.org/vc/) - Read more on [FreeSIWTCH Confluence](https://freeswitch.org/confluence/display/FREESWITCH/Verto+Communicator).

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
