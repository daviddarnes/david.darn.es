---
title: Jekyll Conf Lightening Talk
colour: "#B60000"
icon: person
---

Recently I was asked by [CloudCannon](http://cloudcannon.com/) to record a lightning talk for [Jekyll Conf](http://jekyllconf.com/). It was a great opportunity to contribute to the Jekyll community. You can watch all the talks from the day [on YouTube](https://www.youtube.com/playlist?list=PLrxYIq_0LFJdi2HJ6lnY4nm7ewu221hyS).

<!-- more -->

Below is a video of my lightning talk, as well as a write up of my talk. You can also check out my slides on [Slides.com](http://slides.com/daviddarnes/deck-1).

{% include youtube.html id="Y4qwpN40Dvg" %}

## Doing a lot with a little

Hi I'm David Darnes, and I'm gonna be talking about doing a lot with a little. So I'm web designer and front-end developer and work at [BaseKit](http://www.basekit.com/), where we build an online website editor. That is when we're not [mummifying each other](http://slides.com/daviddarnes/deck-1#/2). Overall, I just like building websites, and using the tools online to help me build them. But it got me thinking, how much can we achieve with was essentially not very much?

![lazy]({{ site.url }}/images/jekyll-conf/lazy.gif "lazy"){: style="width: 100%"}

No, this isn't gonna be a talk on how to be lazy or how to cut corners. This is about utilizing the tools that we have online to really build a quite rich website.

So let's begin, and since this is Jekyll Conference we might as well use [Jekyll](http://jekyllrb.com/). And of course using [GitHub Pages](https://pages.github.com/) means that we can host the site and manage it with versioning. But what about an SSL certificate? By using GitHub Pages we do get an SSL, but I want to use a custom domain. So that's why I use [CloudFlare](https://www.cloudflare.com/), and CloudFlare gives me an SSL certificate and a user interface to [control my URLs](http://slides.com/daviddarnes/deck-1/#/6).

Let's talk about content. Jekyll provides us with pages, posts, but what about products? Can we add an ecommerce system to our site? Well we can with [Gumroad](https://gumroad.com/). Gumroad will allow us to add a product directly into our site. All we need to do is add a bit of [JavaScript and a link](http://slides.com/daviddarnes/deck-1/#/8), and that's it. It'll work pretty much like a normal ecommerce site.

![Simple Jekyll Search]({{ site.url }}/images/jekyll-conf/docs-search.gif "Simple Jekyll Search")

Now we have all this content going on, we need a searching method to help our users find stuff they want. There are several tools out there that can add a search to your site. However for me I would use [Simple Jekyll Search](https://github.com/christian-fei/Simple-Jekyll-Search). What this does is give you a live search tool for your site, allowing users to find anything they want.

What about contacting your users, or people who have bought products from your site? Yeah, we could use [Disqus](https://disqus.com/), but what about on a one-to-one basis? Well we can achieve that with [Formspree](https://formspree.io/), which is a really easy way to add contact forms to pretty much any site. I've even [created a tutorial online](http://webdesign.tutsplus.com/tutorials/quick-tip-add-a-formspree-form-to-your-static-sites--cms-23870) that you can use, just follow the link in the slides.

So let's round things up. We've got templating and page generation, hosting, an SSL certificate, ecommerce, site search and contact forms. But some of you might be thinking...

> So what, I've known about these tools already. You're not really telling me anything new

![Benny]({{ site.url }}/images/jekyll-conf/benny.gif "Benny"){: style="width: 100%"}

Well thinking about it. All these tools allow you to build a lot of things. You can do so much with what we have online, the world is our oyster we can build anything we like with not a lot. I'm also pretty grateful that these tools even exist. So thank you to those people who have made all these tools and help me to build things every day, and I'd like to thank you for watching... (reading).
