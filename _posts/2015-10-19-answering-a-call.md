---
layout: page
title: "Answering a Call"
category: tut
date: 2015-10-19 13:23:21
disqus: 2015-10-19-answering-a-call
order: 6
---

## Receiving a call event

```javascript
vertoCallbacks = {
  onWSLogin: onWSLogin,
  onWSClose: onWSClose,
  onDialogState: onDialogState
};

function onDialogState(dialog) {
  console.debug('onDialogState', dialog);
  
  if(!currentCall) {
    currentCall = dialog;
  }
  
  if(dialog.state.name == 'ringing') {
    alert('Someone is calling you, answer!');
  }
};
```

## Preparing interface

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <button id="make-call">Make call</button>
  <button id="hang-up-call">Hang up call</button>
  <button id="answer-call">Answer call</button>
</div> <!-- /container -->
```

## Binding click

Inside our bootstrap function add event bindings with a function callback so that we know when user clicked our Answer Call button:

```javascript
function bootstrap(status) {
  // ...
  document.getElementById("make-call").addEventListener("click", makeCall);
  document.getElementById("hang-up-call").addEventListener("click", hangupCall);
  document.getElementById("answer-call").addEventListener("click", answerCall);
};
```

## Answering a call

We have to create the callback we've specified to the event binding inside our main function. The answer function is (also) the easiest possible, since Verto session object already implements it.

```javascript
function answerCall() {
  currentCall.answer();
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
    document.getElementById("answer-call").addEventListener("click", answerCall);
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
      userVariables: {
        avatar: "",
        email: "test@test.com"
      }
    });
  };
  
  function hangupCall() {
    currentCall.hangup();
  };
  
  function answerCall() {
    currentCall.answer();
  };
  
  vertoCallbacks = {
    onWSLogin: onWSLogin,
    onWSClose: onWSClose,
    onDialogState: onDialogState
  };
  
  function onWSLogin(verto, success) {
    console.log('onWSLogin', success);
  };
  
  function onWSClose(verto, success) {
    console.log('onWSClose', success);
  };
  
  function onDialogState(dialog) {
    console.debug('onDialogState', dialog);
    
    if(!currentCall) {
      currentCall = dialog;
    }
    
    if(dialog.state.name == 'ringing') {
      alert('Someone is calling you, answer!');
    }
  };
})();
```

Now you can answer calls in our Verto demo app. What about [Add Video Support](/tut/adding-video-support.html)?
