---
title: "Could GitHub Make a CMS?"
colour: "#4078c0"
---

Following on from [my previous article](https://david.darn.es/2016/02/18/using-the-github-com-interface/), I wanted to explore the idea of GitHub making a CMS. What would it be? How would it work? Why would they even do it?

To break down this hypothetical concept I'm going to use the [Five Ws](https://en.wikipedia.org/wiki/Five_Ws), otherwise known as "Who, What, Where When and Why?".

## Who?

Well, Github of course. That was easy... Actually, let's use this opportunity to look at who else has made a CMS for GitHub (or at least integrates with GitHub repos):

- [CloudCannon](http://cloudcannon.com/): It ticks all the boxes of what you'd expect from a CMS that works with Jekyll & GitHub Pages. [Posts](http://docs.cloudcannon.com/editing/blogging/), [pages](http://docs.cloudcannon.com/editing/content-editor/), [metadata](http://docs.cloudcannon.com/editing/front-matter/), everything is available in their UI. In addition you can use an `editable` class name to give control over that content in the UI.

- [Siteleaf](http://www.siteleaf.com/): This is a CMS that can publish to GitHub Pages, however it doesn't use Jekyll. The content editor has some [really nice features](http://www.siteleaf.com/blog/markdown-in-siteleaf/). What interests me most is [v2 of it](http://v2.siteleaf.com/), which brings it right inline with the full GitHub ecosystem.

- [prose.io](http://prose.io/): Prose is an extremely clever [JavaScript project on Github](https://github.com/prose/prose). You simply authorise it with your GitHub account and you're off.

- [DIY](https://pages.github.com/): Well you know the score. Clone your site down, edit your content with whatever application you like, and then push it back up. Simple, works but not the experience you're looking for.

So these are what GitHub would be sort of contending with. They would take nods from prose mostly, as it's more like an web editor mask over the underlying code. They could take from CloudCannon as well, in the ways they present front matter as page options. Siteleaf has something they'd definitely want, drag and drop content adding. GitHub already implemented file uploading with drag and drop, but Siteleaf takes it a step further by allowing text files to be dragged straight into the main text area of posts and pages.

## What

Now that we've done a bit of competitor research we can start to piece together what the CMS might be like.

## Where

A good question really, would they add it into the mix on GitHub.com? Or would they try to do what prose.io has done, and split it off to it's own product that links with your GitHub account?

## When

How far down the roadmap is this feature, if at all.

## Why

Why would they make it? I'm not sure if they even would.
