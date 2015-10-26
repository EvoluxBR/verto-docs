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
```

Now you should be able to make an audio call with Verto. But if you're able to make a new call you should be able do [Hang up a Call]({{ site.baseurl }}/tut/hanging-up-a-call.html).
