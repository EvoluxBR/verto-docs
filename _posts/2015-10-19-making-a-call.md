---
layout: page
title: "Making a Call"
category: tut
date: 2015-10-19 13:23:05
disqus: 2015-10-19-making-a-call
order: 4
---

Since we've got a Verto client working and connected to a Verto server, it's time to make an audio call.

## Building interface

Let's keep things simple and just add a button:

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <button id="make-call">Make call</button>
</div> <!-- /container -->
```

## Binding click

Inside our bootstrap function add event bindings with a function callback so that we know when user clicked our Make Call button:

```javascript
function bootstrap(status) {
  // ...
  document.getElementById("make-call").addEventListener("click", makeCall);
};
```

## Specifying current call variable

We need to store our call session in somewhere if we need to reuse it later. Let's add it to our main function variables:

```javascript
var vertoHandle, vertoCallbacks, currentCall;
```

## Making a call

We have to create the callback we've specified to the event binding inside our main function.

```javascript
function makeCall() {

  currentCall = vertoHandle.newCall({
    // Extension to dial.
    destination_number: '3520',
    caller_id_name: 'Test Guy',
    caller_id_number: '1008',
    outgoingBandwidth: 'default',
    incomingBandwidth: 'default',
    // Enable stereo audio.
    useStereo: true,
    // Set to false to disable inbound video.
    useVideo: true,
    // You can pass any application/call specific variables here, and they will
    // be available as a dialplan variable, prefixed with 'verto_dvar_'.
    userVariables: {
      // Shows up as a 'verto_dvar_email' dialplan variable.
      email: 'test@test.com'
    },
    // Use a dedicated outbound encoder for this user's video.
    // NOTE: This is generally only needed if the user has some kind of
    // non-standard video setup, and is not recommended to use, as it
    // dramatically increases the CPU usage for the conference.
    dedEnc: false,
    // Example of setting the devices per-call.
    //useMic: 'any',
    //useSpeak: 'any',
  });
};
```

## Tracking call progress

The ```onDialogState``` callback can be used to track the progress of the call
if desired. It's fired each time the call changes state.

```javascript
// Receives call state messages from FreeSWITCH.
function onDialogState(d) {
  switch (d.state.name) {
    case "trying":
      break;
    case "answering":
      break;
    case "active":
      break;
    case "hangup":
      log("Call ended with cause: " + d.cause);
      break;
    case "destroy":
      // Some kind of client side cleanup...
      break;
  }
}

vertoCallbacks = {
  onDialogState: onDialogState,
  // Other callbacks...
};
```

Now you should be able to make an audio call with Verto. But if you're able to make a new call you should be able to [hang up a call]({{ site.baseurl }}/tut/hanging-up-a-call.html).

You also may be interested in [receiving real-time updates from the conference]({{ site.baseurl }}/tut/subscribing-to-the-live-array.html).
