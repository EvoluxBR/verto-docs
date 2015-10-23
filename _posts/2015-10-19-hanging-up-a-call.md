---
layout: page
title: "Hanging Up a Call"
category: doc
date: 2015-10-19 13:23:12
disqus: 2015-10-19-hanging-up-a-call
order: 5
---

Since we've got a Verto client working and connected to a Verto server, it's time to make an audio call.

## Building interface

Let's keep things simple and (again) just add a button:

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <button id="make-call">Make call</button>
  <button id="hang-up-call">Hang up call</button>
</div> <!-- /container -->
```

## Binding click

Inside our bootstrap function add event bindings with a function callback so that we know when user clicked our Make Call button:

```javascript
function bootstrap(status) {
  // ...
  document.getElementById("make-call").addEventListener("click", makeCall);
  document.getElementById("hang-up-call").addEventListener("click", hangupCall);
};
```

## Hanging up a call

We have to create the callback we've specified to the event binding inside our main function. The hangup function is the easiest possible, since Verto session object already implements it.

```javascript
function hangupCall() {
  currentCall.hangup();
};
```

## Full code

In the end we should see something like this in out `main.js` file:

```javascript
(function() {
  var vertoHandle, vertoCallbacks, currentCall;
  
  $.verto.init({}, bootstrap);
  
  function bootstrap(status) {
    vertoHandle = new jQuery.verto({
      login: '1008@127.0.0.1',
      passwd: '1234',
      socketUrl: 'wss://127.0.0.1:8082',
      ringFile: 'sounds/bell_ring2.wav',
      deviceParams: {
        useMic: true,
        useSpeak: true
      },
      iceServers: true
    }, vertoCallbacks);
    
    document.getElementById("make-call").addEventListener("click", makeCall);
    document.getElementById("hang-up-call").addEventListener("click", hangupCall);
  };
  
  function makeCall() {
    currentCall = vertoHandle.newCall({
      destination_number: "3520",
      caller_id_name: "Test Guy",
      caller_id_number: "1008",
      outgoingBandwidth: "default",
      incomingBandwidth: "default",
      useStereo: true,
      useMic: true,
      useSpeak: true,
      dedEnc: false,
      mirrorInput: true,
      userVariables: {
        avatar: "",
        email: "test@test.com"
      }
    });
  };
  
  function hangupCall() {
    currentCall.hangup();
  };
  
  vertoCallbacks = {
    onWSLogin: onWSLogin,
    onWSClose: onWSClose
  };
  
  function onWSLogin(verto, success) {
    console.log('onWSLogin', success);
  };
  
  function onWSClose(verto, success) {
    console.log('onWSClose', success);
  };
})();
```

Now that you're able to make and hang up a call wit Verto, what about [Adding Video Support](/doc/adding-video-support.html)?.
