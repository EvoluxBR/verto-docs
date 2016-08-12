---
layout: page
title: "Sending DTMF"
category: tut
date: 2016-08-11 17:58:19
disqus: 2016-08-11-sending-dtmf
order: 14
---

An example of sending DTMF for the logged in user.

In the example code below, ```currentCall``` is an instance of ```vertoHandle.newCall()```
as created in [making an audio call]({{ site.baseurl }}/tut/making-a-call.html).

```javascript
// The sent key digits map to the <caller-controls> section of
// conference.conf.xml
var memberMute = function() {
  // Normally audio mute/unmute.
  currentCall.dtmf("0");
  // Normally video mute/unmute.
  currentCall.dtmf("*0");
}
```

