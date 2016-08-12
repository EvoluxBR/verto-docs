---
layout: page
title: "Sending conference commands"
category: tut
date: 2016-08-11 17:58:19
disqus: 2016-08-11-sending-conference-commands
order: 13
---

It's possble to control various aspects of the conference by sending
conference commands directly from Verto.

In the example code below, ```vertoConf``` is an instance of ```$.verto.conf```
as created in [subscribing to the live array]({{ site.baseurl }}/tut/subscribing-to-the-live-array.html).

Note that the command will only succeed if the logged in Verto user has
permissions to execute it.

```javascript
// This translates to the following conference API command:
// conference [conference id] [command] [id] [value]
var sendCommand = function (command, id, value) {
  vertoObj.rpcClient.call("verto.broadcast", {
    "eventChannel": vertoConf.params.laData.modChannel,
    "data": {
      "application": "conf-control",
      "command": command,
      "id": id,
      "value": value
    }
  });
}

// Some examples of using the above sendCommand() function.
var toggleAudioMute = function(conferenceUserId, arg) {
  sendCommand('tmute', conferenceUserId, arg);
}
var toggleVideoMute = function(conferenceUserId, arg) {
  sendCommand('tvmute', conferenceUserId, arg);
}
var videoLayout = function(layoutId) {
  sendCommand("vid-layout", null, layoutId);
}
```

