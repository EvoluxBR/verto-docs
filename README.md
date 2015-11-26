# Verto documentation

Verto documentation uses markdown and is built with Jekyll, a simple, blog-aware, static site generator perfect for personal, project, or organization sites. View it live [clicking here](http://evoluxbr.github.io/verto-docs/).

## Installing Jekyll

Jekyll is a Ruby Gem. To install it, simply run the following command:

```shell
gem install jekyll --no-doc
```

`--no-doc` optional parameter will ignore documentation files. You still can access Jekyll documentation online: [Jekyll Documentation](https://jekyllrb.com/docs/home/).

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
