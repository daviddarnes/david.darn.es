---
title: Oi, GitHub.io
redirect_from: /website/hi-world/
---

I've decided to follow the cool kids and start up a proper [github.io](https://pages.github.com/) site. For the time being I'll be leaving it at [daviddarnes.github.io](https://daviddarnes.github.io). However I'd like to slowly transfer the articles from my current WordPress site to this one, with the plan to eventually move entirely over to this system and archive the WordPress site. The switch to this was inevitable really. I dabbled with the idea, thinking it was pretty cool that I could not only have my whole site open source, but also be able to host it from the same place as well.
<!-- more -->

### To Do
- **Transfer articles from the WordPress site to here:**
  I'll try out this [WordPress to Jekyll export plugin](https://github.com/benbalter/wordpress-to-jekyll-exporter), but if it's not in a format I like I'll probably copy them out manually. There's not that many to do.
- **Update my GitHub experiments:**
  I have a couple of experiments I've put on GitHub but not cleaned up properly. I want to use GitHub Pages as a way to demo them.
- **Work on this site's design:**
  It's majorly simple right now, I've worked on the layout and the fun SVG animations but not much else. I could do with working on the typography. The good thing about personal sites is that you can constantly work on them, aka progressive enhancement.

### What is GitHub Pages?

GitHub Pages is a service where you are able to host the static content coming from any of your GitHub repos. This static content all hangs of the subdomain I mentioned above, ```daviddarnes.github.io```. Think of this like your own subdomain, much in the same way tumblr gives you your own subdomain. For example, I have a repo on GitHub called [flynn](https://github.com/daviddarnes/flynn), which means I can host static content from that repo at [daviddarnes.github.io/flynn](https://daviddarnes.github.io/flynn/). To activate this feature in a repo simply create a branch called ```gh-pages```, and of course have some static content to show. [Here's the repo and branch](https://github.com/daviddarnes/flynn/tree/gh-pages) that is used for the flynn page.

### So how does this site work?

Good question. All repos on GitHub require that you create a ```gh-pages``` branch in order to activate the static content hosting features. However to host content on the main subdomain you need to create a repo called ```username.github.io```, but replacing username with your username, or organisation name. By creating this you activate the subdomain content hosting. [Here's the repo for this site](https://github.com/daviddarnes/daviddarnes.github.io), note that if you look in the branches you'll see that there isn't a ```gh-pages```. This isn't needed, by creating the repo with that particular name you're activating the feature, the content from the master branch is then used for the content.

I hope this gives you an insight into my plans for this site and a little useful info on GitHub Pages and how to get it working.

Cheers, Dave
