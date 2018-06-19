---
layout: page
title: "Adding H264 Support"
category: tut
date: 2018-06-19 16:08:19
disqus: 2018-06-19-adding-h264-support
order: 17
---

While the default configured video codec in Verto is VP8, H264 is also
supported, and requires just a few small configuration changes.


## Build/load mod_av

mod_av is required for H264 to work properly:

1. In ```modules.conf``` in the FreeSWITCH source directory, uncomment mod_av
2. ```make && make install```
3. In ```conf/autoload_configs/modules.conf.xml``` uncomment mod_av (enables
    auto loading of the module)
4. Restart FreeSWITCH


## Disable mod_h26x

mod_h26x was used in previous versions of FreeSWITCH for passthrough video,
and can cause problems with Verto's H264 implmentation, so it should be
disabled.

Check ```conf/autoload_configs/modules.conf.xml``` and make sure mod_h26x is
*not* enabled. If it is, comment out that line and restart FreeSWITCH.


## Configure Verto for h264 support

Edit ```conf/autoload_configs/verto.conf.xml``` and add ```h264``` to the
```outbound-codec-string``` and ```inbound-codec-string``` profile parameters
for all profiles you wish to have H264 enabled:

```xml
<param name="outbound-codec-string" value="opus,vp8,h264"/>
<param name="inbound-codec-string" value="opus,vp8,h264"/>
```

Codecs are tried in the order they are specified in the parameter.
