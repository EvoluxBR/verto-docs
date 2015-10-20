---
layout: page
title: "Installing Verto"
category: doc
date: 2015-10-19 11:56:05
disqus: 2015-10-19-installing-verto
---

Before we can use Verto, we'll need to install it. There are two options available:

- Install FreeSWITCH + Verto
- Install Verto only

If you're going to use a self hosted FreeSWITCH server you can just use the [Freeswitch/Verto Installation Guide](https://freeswitch.org/confluence/display/FREESWITCH/FreeSWITCH+1.6+Video) as it already comes with Verto.

If you have an external FreeSWITCH server with mod_verto enabled and wish to use Verto stand-alone, follow the next steps.

## Requirements

We need to install [Node.js](https://nodejs.org/) in order to have access to its package manager, npm.

## Installing

With Node.js installed and Node Package Manager available, run the following command:

```
npm install verto
```
