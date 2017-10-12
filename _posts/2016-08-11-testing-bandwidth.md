---
layout: page
title: "Testing bandwidth"
category: tut
date: 2016-08-11 17:58:19
disqus: 2016-08-11-testing-bandwidth
order: 16
---

Since users can be operating under a wide variety of network conditions, it
can be very helpful to perform a test to determine their bandwidth capacity.

Fortunately, Verto makes this easy with a built-in bandwidth testing method.

## Performing the test

The test can be performed any time after the user has logged into the server.

```javascript
var bandwidthTestData;
var testBandwidth = function() {
  // Translates to 256KB.
  var bytesToSendAndReceive = 1024 * 256;
  vertoHandle.rpcClient.speedTest(bytesToSendAndReceive, function(event, data) {
    // These values are in kilobits/sec.
    var upBand = Math.ceil(data.upKPS);
    var downBand = Math.ceil(data.downKPS);
    console.log('[BANDWIDTH TEST] Up: ' + upBand + ', Down: ' + downBand);
    // Store the results for later.
    bandwidthTestData = data;
  });
}
```

## Passing test results in new calls

Data returned from a bandwidth test can be used to set specific values for
the ```incomingBandwidth``` and ```outgoingBandwidth``` call parameters, which
will be used to calculate the best strategy for sending and receiving video
within these bandwidth limits. For example:

```javascript
function makeCall() {
  currentCall = vertoHandle.newCall({
    outgoingBandwidth: bandwidthTestData.upKPS,
    incomingBandwidth: bandwidthTestData.downKPS,
    // Other params...
  });
};
```

## Using test results to calculate video resolution

You also may wish to use the tested upload speed to assist in calculating the
video resolution to send to the server (as set in ```vertoHandle.videoParams```).
