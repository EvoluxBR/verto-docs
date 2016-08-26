# Verto documentation

Verto documentation uses markdown and is built with [Jekyll](https://jekyllrb.com/), a simple, blog-aware, static site generator perfect for personal, project, or organization sites. View it live [clicking here](http://evoluxbr.github.io/verto-docs/).

## Installing dependencies

```shell
bundle install
```

> Note: you may need to use [RVM](https://rvm.io/) to install `ruby` and then execute `gem install bundle` before executing the command above, specially on Mac OS X.

## Running Verto docs server

Inside verto docs directory and after installing Jekyll run:

```shell
jekyll serve
```

Now you can access [http://127.0.0.1:4000/](http://127.0.0.1:4000/) and live preview verto docs while you edit its files. The server auto reloads when something changes.

## Creating new pages

Our documentation follows a very simple convention of defining categories that correspond to sections in the navigation bar. They are:

- doc - Documentation
- ref - Reference
- tut - Tutorial
- dev - Developers

Inside verto docs directory run:

```shell
ruby bin/jekyll-page "Some Doc Page Title" doc
```

## Releasing new versions

- run the command `jekyll build` inside repository on master branch
- copy all content generated inside the `_site` directory to the root of the gh-pages branch
- commit changes in gh-pages branch
