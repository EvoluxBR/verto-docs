---
layout: page
title: "Installing Verto"
category: tut
date: 2015-10-19 11:56:05
disqus: 2015-10-19-installing-verto
order: 2
---

Before we can use Verto, we'll need to install it. There are two options available:

- Install FreeSWITCH + Verto
- Install Verto only

If you're going to use a self hosted FreeSWITCH server you can just use the [FreeSWITCH/Verto Installation Guide](https://freeswitch.org/confluence/display/FREESWITCH/FreeSWITCH+1.6+Video) as it already comes with Verto.

If you have an external FreeSWITCH server with mod_verto enabled or just wish to use Verto stand-alone, follow the next steps.

## Requirements

We need [Node.js](https://nodejs.org/) installed in order to have access to its package manager, **npm**.

## Installing

### Verto 

With [Node.js](https://nodejs.org/) installed and Node Package Manager available, install verto library **inside** `lib/` directory.:

```
npm install verto
```

Verto library should be installed in `lib/node_modules/verto/` directory now.

### Dependencies 

Verto depends on jQuery and jQuery JSON, so let's install them too:

```
npm install jquery
npm install jquery-json
```

[Next step is import and initialize Verto in our project](/tut/initializing-verto.html).
