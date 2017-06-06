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

The bootstrap function will connect to the Verto server and log in with specified credentials and configurations.

Replace the values in brackets with the information for your FreeSWITCH and STUN servers.

```javascript
function bootstrap(status) {
  // Create a new verto instance:
  // This step performs a user login to FreeSWITCH via secure websocket.
  // The user must be properly configured in the FreeSWITCH user directory.
  vertoHandle = new jQuery.verto({
    login: '[USER]@[YOUR_FREESWITCH_SERVER_DOMAIN]',
    passwd: '[PASSWORD]',
    // As configured in verto.conf.xml on the server.
    socketUrl: 'wss://[YOUR_FREESWITCH_SERVER_DOMAIN]:8082',
    // TODO: Where is this file, on the server? What is the base path?
    ringFile: 'sounds/bell_ring2.wav',
    // STUN/TURN server config, more than one is allowed.
    // Instead of an array of objects, you can also pass a Boolean value,
    // false disables STUN, true uses the default Google STUN servers.
    iceServers: [
      {
        url: 'stun:[YOUR_STUN_SERVER]',
      },
    ],
    // These can be set per-call as well as per-login.
    deviceParams: {
      useMic: 'any',
      useSpeak: 'any',
    },
    // Optional Id of the HTML audio/video tag to be used for playing video/audio.
    // This can even be a function which will return an element id. (Use this as
    // function to create unique element for every new call specially when dealing
    // with multiple calls simultaneously to avoid conflicts between streams.
    // In this case, once call is finished, newly generated element will be
    // destroyed automatically)
    tag: "video-container",
    // Below are some more advanced configuration parameters.
    // Google Chrome specific adjustments/filters for audio.
    // Official documentation is scant, best to try them out and see!
    //audioParams: {
    //  googEchoCancellation: true,
    //  googAutoGainControl: true,
    //  googNoiseSuppression: true,
    //  googHighpassFilter: true,
    //  googTypingNoiseDetection: true,
    //  googEchoCancellation2: false,
    //  googAutoGainControl2: false,
    //},
    // Internal session ID used by Verto to track the call, eg. for call
    // recovery. A random one will be generated if none is provided, and,
    // it can be useful to provide a custom ID to store and reference for
    // other purposes.
    //sessid: sessid,
  }, vertoCallbacks);
};
```

## Callbacks

Almost everything that happens in Verto fires an event. So we need event handlers to receive and process these events.

At first we'll handle the login event:

```javascript
function onWSLogin(verto, success) {
  console.log('onWSLogin', success);
  if (success) {
    // At this point you're connected to the FreeSWITCH server and logged
    // in, ready to place a call to the conference, or run a test for the
    // user's bandwidth.
  }
};
```

When we add it to the Verto Callbacks dictionary it will print the ```success``` variable value on browser's console when web socket login task is finished.

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
      // The params...
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

If everything went fine you should see a console log with `onWSLogin true` and can now [make a call]({{ site.baseurl }}/tut/making-a-call.html), or [test your bandwidth]({{ site.baseurl }}/tut/testing-bandwidth.html).
