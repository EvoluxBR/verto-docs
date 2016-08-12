---
layout: page
title: "Sending chat messages"
category: tut
date: 2016-08-11 17:58:19
disqus: 2016-08-11-sending-chat-messages
order: 15
---

An example of sending a chat message from the logged in user.

In the example code below, ```vertoConf``` is an instance of ```$.verto.conf```
as created in [subscribing to the live array]({{ site.baseurl }}/tut/subscribing-to-the-live-array.html).

```javascript
var sendConferenceChat = function(message) {
  // The second argument is a message type, completely arbitrary, can be used
  // classify different kinds of messages.
  vertoConf.sendChat(message, "message");
}
```

