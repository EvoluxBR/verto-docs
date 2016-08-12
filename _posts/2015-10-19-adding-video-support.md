---
layout: page
title: "Adding Video Support"
category: tut
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
    // ID of HTML video tag where the video feed is placed.
    tag: "video-container",
    deviceParams: {
      // Asking for camera permissions and devices.
      useCamera: 'any',
      useMic: 'any',
      useSpeak: 'any',
    },
    // Other params...
  }, vertoCallbacks);
};
```

## Editing makeCall

```javascript
function makeCall() {

  // Sets the parameters for the video stream that will be sent to the
  // videoconference.
  // Hint: Use the upKPS result from a bandwidth test to determine the video
  // resolution to send!
  vertoHandle.videoParams({
    // Dimensions of the video feed to send.
    minWidth: 320,
    minHeight: 240,
    maxWidth: 640,
    maxHeight: 480,
    // The minimum frame rate of the client camera, Verto will fail if it's
    // less than this.
    minFrameRate: 15,
    // The maximum frame rate to send from the camera.
    vertoBestFrameRate: 30,
  });

  currentCall = vertoHandle.newCall({
    // Enable video support.
    useVideo: true,
    // Mirror local user's webcam.
    mirrorInput: true,
    // Other params...
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

And if something fails, your internet connection goes down for a while or you browser crashes? [Recovering a call]({{ site.baseurl }}/tut/recovering-a-call.html) looks like something more complex to do, doesn't?
