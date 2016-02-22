---
title: "Could GitHub Make a CMS?"
colour: "#4078c0"
---

Following on from [my previous article](https://david.darn.es/2016/02/18/using-the-github-com-interface/), I wanted to explore the idea of GitHub making a CMS. What would it be? How would it work? Why would they even do it?

**To break down this hypothetical concept I'm going to use the [Five Ws](https://en.wikipedia.org/wiki/Five_Ws), otherwise known as "Who, What, Where When and Why?".**

<!-- more -->

## Who?

Well, GitHub of course. That was easy... Actually, let's use this opportunity to look at who else has made a CMS for GitHub Pages:

- ![cloudcannon]({{ site.url }}/images/github-cms/cloudcannon.png "cloudcannon")
  **[CloudCannon](http://cloudcannon.com/):** CloudCannon ticks all the boxes of what you'd expect from a CMS that works with Jekyll & GitHub Pages. [Posts](http://docs.cloudcannon.com/editing/blogging/), [pages](http://docs.cloudcannon.com/editing/content-editor/), [metadata](http://docs.cloudcannon.com/editing/front-matter/), everything is available in their UI. In addition you can use an `editable` class name to give control over that content in the UI.

- ![siteleaf]({{ site.url }}/images/github-cms/siteleaf.jpg "siteleaf")
  **[Siteleaf](http://www.siteleaf.com/):** This is a CMS that can publish to GitHub Pages, however it doesn't use Jekyll. The content editor has some [really nice features](http://www.siteleaf.com/blog/markdown-in-siteleaf/). What interests me most is [v2 of the CMS](http://v2.siteleaf.com/), which brings it right inline with the full GitHub ecosystem.

- ![prose]({{ site.url }}/images/github-cms/prose.png "prose")
  **[prose.io](http://prose.io/):** Prose is an extremely clever [JavaScript project on Github](https://github.com/prose/prose). You simply authorise it with your GitHub account and you're off.

- **[DIY](https://pages.github.com/):** Well you know the score. Clone your site down, edit your content with whatever application you like, and then push it back up. Simple, works but not the experience you're looking for.

So these are what GitHub would be sort of contending with. There's lots of interesting features in all of these CMSs. Prose has quite a sparse UI, allowing you to focus on what you're writing. I like how CloudCannon presents front matter, essentially turning it into custom fields for your pages and posts. The drag and drop feature in Siteleaf is really clever, which conveniently lines up with their new drag and drop feature.

## What

Now that we've done a bit of competitor research we can start to piece together what the CMS might be like.

I don't feel like it would be overly complex in execution. They could create something completely independent, but that would be a waste of what they've already implemented into the main product. They have a web interface, markdown editing and now file upload, so why start over?

We're now thinking of something more like an expansion and improvement on the current editor. Less a CMS, more of an **enhanced writing experience**. The drawback to this is that it's not easy for say a client to pick up, which is what other CMSs mentioned above do a lot better.

Lets not forget though, this environment is designed for more regular users of GitHub. It would be easier to focus on helping GitHub users to write, rather than chasing users that are better off using those systems.

## Where

So where would this enhanced editing experience go? Well as mentioned above, it would be mixed into GitHub.com. But where? I've put together some examples that they could implement:

// Image of the top of a markdown editor

Here a new "md" file has triggered the appearance of a markdown editor at the top. Note the file name as well, this could be autofilled when the user creates a new file. This would be based on if the file being created is inside the `_posts` or `_drafts` directory.

// Image of a drag and drop state of an image to the page

The editor could be smart with images as well. Mimicking the drag and drop technique from Siteleaf, when the user drags an image onto the page the image could be uploaded and and the relevant markdown could be inserted to the page.

// Screenshot of Use Canvas

What about improving the markdown presentation? I've been using [Canvas](https://usecanvas.com/) a lot recently and the way it presents markdown content is really clever. Allowing full markdown editing but still showing the resulting copy.

## When

Um, well now? I sadly can't see GitHub's internal roadmap but their feature additions seem to be few and far between. That is until recently, their blog has been a bit more active lately with adding more features.

I would imagine if they did do this it would be one step at a time, adding a feature and then gradually rolling it out. Some might see it as slow development, but with a site of this scale you can't play it safe enough.

## Why

Good question, why bother? As we mentioned above, there's plenty of CMSs out there that are willing to fill that gap. I wouldn't be surprised if more appear in the future. GitHub could not bother with any of this and it'll be no worse off. But what if they did? Would it be something that tips even more users to their platform? Could the combination of Jekyll, GitHub Pages and their easy to use content editor expand their userbase?

This is of course all hypothetical. They would have to do more than what I've covered in this article to achieve the ideas I'm throwing around. I at least hope it's on their radar. For now I'm happy using Atom.

Cheers, Dave
