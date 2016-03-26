---
layout: page
title: "Muting a Call"
category: tut
date: 2016-03-26 17:36:47
disqus: 2016-03-26-muting-a-call
order: 9
---

Each Verto call has three distinct muting actions:

- on: means audio is activated and the call is not muted
- off: means audio is deactivated and the call is muted
- toggle: changes the mute state of the call to the opposite value

## Preparing interface

Adding buttons...

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <!-- ... -->
  <button id="mute-call">Mute call</button>
  <button id="unmute-call">Unmute call</button>
  <button id="mute-unmute-call">Mute/Unmute call</button>
</div> <!-- /container -->
```

## Binding click

Inside our bootstrap function add event bindings with a function callback so that we know when user clicked our Mute buttons:

```javascript
function bootstrap(status) {
  // ...
  document.getElementById("mute-call").addEventListener("click", muteCall);
  document.getElementById("unmute-call").addEventListener("click", unmuteCall);
  document.getElementById("mute-unmute-call").addEventListener("click", muteUnmuteCall);
};
```

## Muting a call

We have to create the callbacks we've specified to the event bindings inside our main function.

```javascript
function muteCall() {
  currentCall.mute("off");
};

function unmuteCall() {
  currentCall.mute("on");
};

function muteUnmuteCall() {
  currentCall.mute("toggle");
};
```

Try it and see what each button can do to the active call.
