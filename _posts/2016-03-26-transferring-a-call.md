---
layout: page
title: "Transferring a Call"
category: tut
date: 2016-03-26 17:58:19
disqus: 2016-03-26-transferring-a-call
order: 11
---

One of the most important telephony feature is the Transfer.
As everything we have done with Verto until now, transferring a call will be easy.

## Preparing interface

Adding button...

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <!-- ... -->
  <button id="unhold-call">Transfer call</button>
</div> <!-- /container -->
```

## Binding click

Inside our bootstrap function add event binding with a function callback so that we know when user clicked our Transfer button:

```javascript
function bootstrap(status) {
  // ...
  document.getElementById("transfer-call").addEventListener("click", transferCall);
};
```

## Transferring a call

We have to create the callback we've specified to the event binding inside our main function.

```javascript
function transferCall() {
  var destinationNumber = prompt("Insert transfer destination number");
  if(destinationNumber) {
    currentCall.transfer(destinationNumber);
  }
};
```

Try it and see by yourself how easy is to transfer a call with Verto library.
