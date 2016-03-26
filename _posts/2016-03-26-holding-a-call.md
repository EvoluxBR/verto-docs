---
layout: page
title: "Holding a Call"
category: tut
date: 2016-03-26 17:52:36
disqus: 2016-03-26-holding-a-call
order: 10
---

We can do something else except muting calls on Verto. We can put them on hold.
It means the user won't hear us. A music on hold will be played instead.

## Preparing interface

Adding buttons...

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <!-- ... -->
  <button id="hold-call">Hold call</button>
  <button id="unhold-call">Unhold call</button>
</div> <!-- /container -->
```

## Binding click

Inside our bootstrap function add event bindings with a function callback so that we know when user clicked our Hold buttons:

```javascript
function bootstrap(status) {
  // ...
  document.getElementById("hold-call").addEventListener("click", holdCall);
  document.getElementById("unhold-call").addEventListener("click", unholdCall);
};
```

## Holding a call

We have to create the callbacks we've specified to the event bindings inside our main function.

```javascript
function holdCall() {
  currentCall.hold();
};

function unholdCall() {
  currentCall.unhold();
};
```

Try it and see what each button can do to the active call.
