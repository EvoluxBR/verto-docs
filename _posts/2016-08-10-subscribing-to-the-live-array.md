---
layout: page
title: "Subscribing to the live array"
category: tut
date: 2016-08-10 17:58:19
disqus: 2016-08-10-subscribing-to-the-live-array
order: 12
---

The live array enables you to receive real time server data in a javascript array.

All users dialed into a conference are added to the live array data on the server,
and Verto clients can choose to subscribe to the live array to receive conference
events. FreeSWITCH handles sending the events to all subscribers. Typical events
include:

 * User join/leave
 * Video/audio mute/unmute
 * Talking
 * Video floor

Support also exists for receiving chat data from the server.

## Preparing to subscribe

A caller must be joined to the live array in order to subscribe to live array
updates.

The ```onMessage``` callback receives general broadcast messages from the
server, including events for when a caller has joined and left the live array.

So, the first step is to add an ```onMessage``` callback to our callbacks object:


```javascript
// Receives conference-related messages from FreeSWITCH.
// Note that it's possible to write server-side modules to send customized
// messages via this callback.
function onMessage(verto, dialog, message, data) {
  switch (message) {
    case $.verto.enum.message.pvtEvent:
      if (data.pvtData) {
        switch (data.pvtData.action) {
          // This client has joined the live array for the conference.
          case "conference-liveArray-join":
            // With the initial live array data from the server, you can
            // configure/subscribe to the live array.
            initLiveArray(verto, dialog, data);
            break;
          // This client has left the live array for the conference.
          case "conference-liveArray-part":
            // Some kind of client-side wrapup...
            break;
        }
      }
      break;
    // TODO: Needs doc.
    case $.verto.enum.message.info:
      break;
    // TODO: Needs doc.
    case $.verto.enum.message.display:
      break;
    case $.verto.enum.message.clientReady:
      // 1.8.x+
      // Fired when the server has finished re-attaching any active sessions.
      // data.reattached_sessions contains an array of session IDs for all
      // sessions that were re-attached.
      break;
  }
}

vertoCallbacks = {
  onMessage: onMessage,
  // Other callbacks...
};
```

## Subscribing

Once the client has joined the live array and received the data from the server,
they can subscribe to events.

```javascript
/*
 * Setting up and subscribing to the live array.
 */
var vertoConf, liveArray;
var initLiveArray = function(verto, dialog, data) {
    // Set up addtional configuration specific to the call.
    vertoConf = new $.verto.conf(verto, {
      dialog: dialog,
      hasVid: true,
      laData: data.pvtData,
      // For subscribing to published chat messages.
      chatCallback: function(verto, eventObj) {
        var from = eventObj.data.fromDisplay || eventObj.data.from || 'Unknown';
        var message = eventObj.data.message || '';
      },
    });
    var config = {
      subParams: {
        callID: dialog ? dialog.callID : null
      },
    };
    // Set up the live array, using the live array data received from FreeSWITCH.
    liveArray = new $.verto.liveArray(vertoObj, data.pvtData.laChannel, data.pvtData.laName, config);
    // Subscribe to live array changes.
    liveArray.onChange = function(liveArrayObj, args) {
      console.log("Call UUID is: " + args.key);
      console.log("Call data is: ", args.data);
      try {
        switch (args.action) {

          // Initial list of existing conference users.
          case "bootObj":
            break;

          // New user joined conference.
          case "add":
            break;

          // User left conference.
          case "del":
            break;

          // Existing user's state changed (mute/unmute, talking, floor, etc)
          case "modify":
            break;

        }
      } catch (err) {
        console.error("ERROR: " + err);
      }
    };
    // Called if the live array throws an error.
    liveArray.onErr = function (obj, args) {
      console.error("Error: ", obj, args);
    };
}
```

## Live array data format

There is currently no documentation for the live array data format, however
it's quite easy to discover it by exercising a javascript debugger on your
implementation of the code above, and inspecting ```args.key``` and ```args.data```.

