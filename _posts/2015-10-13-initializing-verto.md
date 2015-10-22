---
layout: page
title: "Initializing Verto"
category: doc
date: 2015-10-13 16:08:19
disqus: 1
order: 3
---

If this is your first time using Verto lib, you'll have to initialize it and get a lib instance.

```javascript
(function() {
  var vertoHandle, vertoCallbacks;
  
  /*
  * Initialize lib, cooking.
  * steps executed in init:
  * - test media permission
  * - check available devices
  */
  $.verto.init({}, bootstrap);
  
  /**
  * Callback for verto init.
  * @constructor
  * @param {boolean} status - has media permission
  */
  function bootstrap(status) {
    var wsURL = 'wss://' + window.location.hostname + ':8082';

    vertoCallbacks = {};

    vertoHandle = new jQuery.verto({
      login: '1008@127.0.0.1',
      passwd: '1234',
      socketUrl: wsURL,
      tag: '',
      ringFile: '',
    }, vertoCallbacks);
    
    
    // do something in our app 
  };
})();
```
[source code]()

### $.verto.init(options, callback) 

Init check browser condition and media (audio and video) permission for library use.

### jQuery.verto(options, callback) [vertoHandle]

vertoHandle is an **jQuery.verto** instance, it'll connect verto JS with FS mod_verto creating a session. **jQuery.verto** constructor receives options and a callback object. Options will be used to configure verto lib.

verto handle options:

```javascript
{
  login: null,
  passwd: null,
  socketUrl: null,
  tag: null,
  localTag: null,
  videoParams: {},
  audioParams: {},
  loginParams: {},
  deviceParams: {
    onResCheck: null,
    useCamera: null,
    useMic: null,
    useSpeak: null
  },
  userVariables: {},
  iceServers: false,
  ringSleep: 6000,
  sessid: null
}
```

* **login**

    sip login for this verto session.

* **passwd**
    
    sip password for this verto session.

* **socketUrl**
    
    freeswitch websocket url (FS Server)
