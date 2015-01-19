---
layout: post
title: Simple success with Jekyll Now!
---

It was after reading Barry Clark's post on [Build A Blog With Jekyll And GitHub Pages](http://www.smashingmagazine.com/2014/08/01/build-blog-jekyll-github-pages/),
I became fascinated with the idea hacker-style blogging on GitHub. So of course I jumped in.

What is Jekyll anyway?
It's a static site generator for plain text using markdown. There's no database to manage, and great customization options for layouts, permalinks, posts, and more.

First things first, I develop on Windows. Does that make you cringe?

My first hurdle was finding out that [Jekyll wasn't supported on Windows officially](http://jekyllrb.com/docs/windows/).
Ugh, but okay, there's unnofficial support. Turns out installing Ruby was a mess to begin with. I fixed a couple errors before stumbling upon madhur's [Building portable Jekyll for Windows](http://www.madhur.co.in/blog/2013/07/20/buildportablejekyll.html). This sounds awesome right? Aside from modifying some environment variables, it was a breeze. I was able to $ jekyll immediately.

Happy ending right? Well there's a bonus ending. [Turns out Barry Clark introduced a way to create a Jekyll blog without the setup or use of command line!](https://github.com/barryclark/jekyll-now)
