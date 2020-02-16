---
title: "Could GitHub Make a CMS?"
colour: "#d26911"
image: "/images/github-cms/octocat.jpg"
---

Following on from [my previous article](https://david.darn.es/2016/02/18/using-the-github-com-interface/), I wanted to explore the idea of GitHub making a CMS. What would it be? How would it work? Why would they even do it?

**To break down this hypothetical concept, I'm going to use the [Five Ws](https://en.wikipedia.org/wiki/Five_Ws), otherwise known as "Who, What, Where, When and Why?".**

<!-- more -->

## Who?

Well, GitHub of course. That was easy...

Actually, let's use this opportunity to look at who else has made a CMS for GitHub Pages:

### [CloudCannon](https://cloudcannon.com/)

![cloudcannon](/images/github-cms/cloudcannon.png "cloudcannon")
CloudCannon ticks all the boxes of what you'd expect from a CMS that works with Jekyll & GitHub Pages: [Posts](https://docs.cloudcannon.com/editing/blogging/), [pages](https://docs.cloudcannon.com/editing/content-editor/), [metadata](https://docs.cloudcannon.com/editing/front-matter/); everything is available in their UI. In addition, you can use an `editable` class name to give control over the content in the UI.

### [Siteleaf](https://www.siteleaf.com/)

![siteleaf](/images/github-cms/siteleaf.jpg "siteleaf")
This is a CMS that can publish to GitHub Pages. However, it doesn't use Jekyll. The content editor has some [really nice features](https://www.siteleaf.com/blog/markdown-in-siteleaf/). What interests me most is [v2 of the CMS](https://v2.siteleaf.com/), which brings it right inline with the full GitHub ecosystem.

### [prose.io](https://prose.io/)

![prose](/images/github-cms/prose.png "prose")
Prose is an extremely clever [JavaScript project on Github](https://github.com/prose/prose). You simply authorise it with your GitHub account and you're off.

### [DIY](https://pages.github.com/)

Well, you know the score. Clone your site down, edit your content with whatever application you like, and then push it back up. It's simple, it works, but it's not the experience you're looking for.

If GitHub were to make a CMS, these are what they would have to contend with. There are lots of interesting features in all of these CMS's. Prose has quite a sparse UI, allowing you to focus on what you're writing. I like how [CloudCannon presents front matter](https://docs.cloudcannon.com/editing/front-matter/), essentially turning it into custom fields for your pages and posts. The [drag and drop feature in Siteleaf](https://www.siteleaf.com/blog/markdown-in-siteleaf/) is really clever, which conveniently lines up with GitHub's new drag and drop feature.

## What

Now that we've done a bit of competitor research, we can start to piece together what the CMS might be like.

I don't feel like it should be overly complex in execution. They could create something completely independent, but that would be a waste of what they've already implemented into the main product. They already have a web interface, markdown editing and now file upload, so why start over?

We're now thinking of something more like an expansion and improvement on the current editor. Less a CMS, more of an **enhanced writing experience**. The drawback to this is that it's not easy for a client to pick up, which is what the other CMS's mentioned above do very well.

Let's not forget, though, that this environment is designed for more regular users of GitHub. It would be easier to focus on helping GitHub users to write, rather than chasing users that are better off using those other systems.

## Where

So, where would this enhanced editing experience go? Well, as mentioned above, it would be mixed into GitHub.com, but where? I've put together some examples that they could implement:

![file markdown editor](/images/github-cms/markdown-editor.png "file markdown editor")[Enlarge](https://github.com/daviddarnes/david.darn.es/blob/gh-pages/images/github-cms/markdown-editor.png)

Here a new "md" file has triggered the appearance of a markdown editor at the top. Note the file name, as well. This could be autofilled when the user creates a new file, based on if the file being created is inside the `_posts` or `_drafts` directory.

![editor drag and drop images](/images/github-cms/editor-drag-drop.png "editor drag and drop images")[Enlarge](https://github.com/daviddarnes/david.darn.es/blob/gh-pages/images/github-cms/editor-drag-drop.png)

The editor could be smart with images, too. Mimicking the drag and drop technique from Siteleaf, when the user drags an image onto the page, the image could be uploaded and and the relevant markdown could be inserted to the page.

![canvas markdown editor](/images/github-cms/use-canvas.gif "canvas markdown editor")

What about improving the markdown presentation? I've been using [Canvas](https://usecanvas.com/) a lot recently and the way it presents markdown content is really clever; this allows full markdown editing, but still shows the resulting copy.

## When

Um, well, now? I sadly can't see GitHub's internal roadmap, but their feature additions seem to be few and far between. That is, until recently. [Their blog](https://github.com/blog/) has been a bit more active lately with adding more features.

I would imagine if they did do this, it would be one step at a time, adding a feature and then gradually rolling it out. Some might see it as slow development, but with a site of this scale, you can't play it safe enough.

## Why

Good question. Why bother? As we mentioned above, there are plenty of CMS's out there that are willing to fill the gap. I wouldn't be surprised if more appear in the future. GitHub could not bother with any of this and they'll be no worse off. But, what if they did? Would it be something that tips even more users to their platform? Could the combination of Jekyll, GitHub Pages and their easy-to-use content editor expand their userbase?

My thinking is, of course, all hypothetical. They would have to do more than what I've covered in this article to achieve the ideas I'm throwing around. I hope it's at least on their radar. For now, I'm happy using Atom.

Cheers, Dave
