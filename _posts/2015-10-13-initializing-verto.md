---
layout: page
title: "Initializing Verto"
category: tut
date: 2015-10-13 16:08:19
disqus: 2015-10-13-initializing-verto
order: 3
---

It's time to edit our `main.js` JavaScript file. Start with the following structure:

```javascript
// our main function
(function() {
  var vertoHandle, vertoCallbacks;
  // put your code here!
})();
```

## Initializing

Initializing Verto will prepare the browser for WebRTC requiring and testing media permissions and checking for available devices.

```javascript
$.verto.init({}, bootstrap);
```

## Bootstrapping

Bootstrap function will connect to Verto server and log in with specified credentials and configurations.

```javascript
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
};
```

## Callbacks

Almost everything that happens in Verto fires an event. So we need event handlers to receive and process these events.

At first we'll handle the login event:

```javascript
function onWSLogin(verto, success) {
  console.log('onWSLogin', success);
};
```

When we add it to the Verto Callbacks dictionary it will print success variable value on browser's console when web socket login task is finished.

```javascript
vertoCallbacks = {
  onWSLogin: onWSLogin,
};
```

You can do the same to the `onWSClose` event. Do not forget to add it to the vertoCallbacks dictionary.

## Full code

In the end of this section you should have something like this in your JavaScript file:

```javascript
(function() {
  var vertoHandle, vertoCallbacks;
  
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

## Modifying HTML

How is this code supposed to work if we don't include Verto and its dependencies in our HTML file? Edit your `index.html` file so that it looks like this:

```html
<!-- Verto dependencies -->
<script src="../lib/node_modules/jquery/dist/jquery.min.js"></script>
<script src="../lib/node_modules/jquery-json/dist/jquery.json.min.js"></script>

<!-- Verto library -->
<script src="../lib/node_modules/verto/src/jquery.verto.js"></script>
<script src="../lib/node_modules/verto/src/jquery.FSRTC.js"></script>
<script src="../lib/node_modules/verto/src/jquery.jsonrpcclient.js"></script>

<!-- Our project's files -->
<script src="main.js"></script>
```

## Trying

We cannot open `index.html` file directly in our browser, since `file:///` protocol won't work properly.

We should access it through a web server. You can user any of them: Apache, nginx... But to keep things simple we'll be using Python bundled Simple HTTP Server inside our project's root directory:

```
python -m SimpleHTTPServer
```

Now you should be able to access [http://127.0.0.1:8000/src/index.html](http://127.0.0.1:8000/src/index.html) and test Verto connection with the browser's console open.

If everything went fine you should see a console log with `onWSLogin true` and can now [Make a Call](/tut/making-a-call.html).
