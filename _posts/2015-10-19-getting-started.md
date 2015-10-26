---
layout: page
title: "Getting Started"
category: tut
date: 2015-10-19 11:49:25
disqus: 2015-10-19-getting-started
order: 1
---

Our project will have the following file structure:

- src/
    - index.html
    - style.css
    - main.js
- lib/
    - node_modules/ `<- Will be covered in next step!`
        - verto/

Let's start adding our basic HTML structure. `index.html` should contain something like this:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Verto - Demo Application</title>
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta name="description" content="Demo Application using Verto jQuery lib.">
    <meta name="author" content="Your name here!">

    <link href="style.css" rel="stylesheet">
  </head>
  
  <body>
    <div class="container">
      <h1>Verto - Demo Application</h1>
    </div> <!-- /container -->
    
    <script src="main.js"></script>
  </body>
</html>
```

jQuery and jQuery JSON are libraries required by Verto jQuery plugin.

[Now, let's install Verto!]({{ site.baseurl }}/tut/installing-verto.html)
