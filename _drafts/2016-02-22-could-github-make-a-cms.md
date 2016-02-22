---
title: "Could GitHub Make a CMS?"
colour: "#4078c0"
---

Following on from [my previous article](https://david.darn.es/2016/02/18/using-the-github-com-interface/), I wanted to explore the idea of GitHub making a CMS. What would it be? How would it work? Why would they even do it?

To break down this hypothetical concept I'm going to use the [Five Ws](https://en.wikipedia.org/wiki/Five_Ws), otherwise known as "Who, What, Where When and Why?".

## Who?

Well, Github of course. That was easy... Actually, let's use this opportunity to look at who else has made a CMS for GitHub (or at least integrates with GitHub repos):


- [CloudCannon](http://cloudcannon.com/): In short, it takes the whole concept of Jekyll and slaps a UI over it. [Posts](http://docs.cloudcannon.com/editing/blogging/), [pages](http://docs.cloudcannon.com/editing/content-editor/), [metadata](http://docs.cloudcannon.com/editing/front-matter/), everything is converted into a simplistic editor interface for the user. It also has a visual editor, allowing developers to target certain pieces of content that they want to be editable.

  I have my reservations though, and sadly it's only skin deep. For some reason the UI doesn't attract me. It doesn't make me think that I, nor my client, will ever understand it entirely.

- [Siteleaf](http://www.siteleaf.com/): This is a CMS that can publish to GitHub Pages, however it doesn't use Jekyll. The content editor has some [really nice features](http://www.siteleaf.com/blog/markdown-in-siteleaf/).

  Despite this, the fact it doesn't work directly with GitHub and Jekyll makes me hesitate to get onboard. What interests me more is [v2 of it](http://v2.siteleaf.com/), which brings it right inline with the full GitHub ecosystem.

- [prose.io](http://prose.io/): Prose is an extremely clever [JavaScript project on Github](https://github.com/prose/prose). You simply authorise it with your GitHub account and you're off. In terms of scale, Prose fits perfectly with my needs.

  There is some gripes I have with it, not because of bugs but more unexpected outcomes when in normal use. I won't go into detail but I hope you understand my point.

- [Contentful](https://www.contentful.com/): You've got your content in one place, and your site on GitHub. This is how it would be if you used Contentful. It's essentially a place to organise and manage content for anything. There is a way to link it with Jekyll, but not Jekyll on GitHub Pages by the looks of it. So they puts it out of the running.

- DIY: Well you know the score. Clone your site down, edit your content with whatever application you like, and then push it back up. Simple, works but not the experience you're looking for.
