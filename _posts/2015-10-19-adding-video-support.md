---
layout: page
title: "Adding Video Support"
category: doc
date: 2015-10-19 13:23:35
disqus: 2015-10-19-adding-video-support
order: 7
---

Verto was built for video conferences, so adding support for it is very simple.

## Preparing interface

```html
<div class="container">
  <h1>Verto - Demo Application</h1>
  <button id="make-call">Make call</button>
  <button id="hang-up-call">Hang up call</button>
  <button id="answer-call">Answer call</button>
  <video id="video-container" autoplay="autoplay" class="video-style"></video>
</div> <!-- /container -->
```

## Editing bootstrap

```javascript
function bootstrap(status) {
  vertoHandle = new jQuery.verto({
    login: '1008@127.0.0.1',
    passwd: '1234',
    socketUrl: 'wss://127.0.0.1:8082',
    ringFile: 'sounds/bell_ring2.wav',
    tag: 'video-container', // specifying video tag in our html
    deviceParams: {
      useCamera: true, // asking for camera permissions and devices
      useMic: true,
      useSpeak: true
    },
    iceServers: true
  }, vertoCallbacks);
};
```

## Editing makeCall

```javascript
function makeCall() {
  currentCall = vertoHandle.newCall({
    destination_number: "3520",
    caller_id_name: "Test Guy",
    caller_id_number: "1008",
    outgoingBandwidth: "default",
    incomingBandwidth: "default",
    useVideo: true, // telling verto to make a call with video support
    mirrorInput: true, // telling verto to mirror user's webcam
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

## Styling video tag

Add something like this to your `style.css` file. Feel free to change and improve it with your taste.

```css
.video-style {
  width: 100%;
  height: 100%;
  object-fit: inherit;
}
```

Now you have full video support in Verto :)

And if somethings fails, your internet connection goes down for a while or you browser crashes? [Recovering a Call](/doc/recovering-a-call.html) looks like something more complex to do, doesn't?
