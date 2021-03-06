---
title: "What Do We Look For In A CMS?"
icon: article
colour: "#4990E2"
excerpt: "I posed this question in several forms on Twitter to get feedback from the community. After some consideration, polls and great discussion, I came up with a list of aspects that people consider when looking for a CMS."
image: "/images/look-for-in-cms/cms-header.jpg"
---

Back in March 2015, I attempted to build [Bread.li](https://bread.li), a site dedicated to providing valuable information on a wide range of CMS's. Without going into too much detail, I failed to complete it and now it's a half baked project :cry:.

So, what went wrong? Well, I think it's down to where I started. I began with the build, rather than the purpose of the site, which is something that often happens when we pick a CMS. **We look at the development benefits over how the CMS will be actually used.**

Allow me to start this side project reboot on the right footing with a better proposal: **what should we look for in a CMS?** I posed [this question](https://daviddarnes.typeform.com/to/V0w4FE) in [several forms](https://twitter.com/DavidDarnes/status/822777330414272513) on Twitter to get feedback from the community. After some consideration, polls and great discussion, I came up with a list of aspects that people consider when looking for a CMS. Bear in mind, **this isn't a definitive list**; there are things missing and some may not be in the order that they _should_ be in, so feel free to send me a tweet with your thoughts.

In priority order:

## 1. Does it fit the client's requirements?

Seems obvious, but it doesn't actually feel like people consider this when they begin working with a new client. Often, our good old friend [WordPress](https://wordpress.org) will fit 90% of cases and we then never break away from that. I'm glad this came out as number 1 as it allows me to explain the two sides I see with fitting the clients needs.

On one hand, we have a specific type of content to deliver, whether those are pages, blog posts or just a single page with an address on it. On the other hand, we have a client that needs something to handle (a.k.a. "manage") said content. When I consider these two sides, I think of the blogging platform [Ghost](https://ghost.org), because it's designed to _deliver_ blog post content and the admin UI is designed to _handle_ blog content.

![Ghost's admin UI and resulting post](/images/look-for-in-cms/ghost-admin.jpg)


## 2. Is there good documentation?

This point came up higher than I expected. From my experience of developing the [Anchor CMS documentation](https://docs.anchorcms.com), I know that poor documentation can turn away a developer almost immediately. An undocumented piece of code might stop a developer using a feature, which in turn means they can't provide it for the client.

However, it's too easy to get blinkered by this aspect. A thriving development community doesn't necessarily mean the CMS is the best for your client. Look for **good** documentation, not _perfect_. Don't forget, adding to the documentation is always a good way to contribute to that community.

## 3. Is the UI easy to understand & use?

Personally, I feel like this point is more important than extensive documentation. A good UI to edit content is pretty much the whole reason we use a CMS so that our clients can understand and use what we have built for them. The CMS interface is the translator that sits between the client and the raw data.

I've seen many cases where this aspect has been considered _after_ most of the CMS has been built. This is then reflected when the CMS has been presented to the developer, where the implementation method and technical features are promoted over the usability.

It's wise to spend some time researching the interface. Try a demo for yourself or even give one to your client to try out.

![Anchor CMS header](/images/look-for-in-cms/anchor-cms-header.jpg)

The screenshot above is of the Anchor CMS header bar, which shows quite a few options, but are clearly labelled and aren't as cluttered as other admin navigations.

## 4. Does it have good performance?

Having a performant CMS is a somewhat overlooked aspect. To be honest, I haven't considered it much in the past. Having a fast performing customer facing site is important and something I like to work on, but what about a performant admin interface?

A good CMS can meet this requirement on two accounts: using the right templating language and caching methods can result in good site speeds, and a fast serving admin interface can make the client feel more confident in editing their site. I know this has been a strong reason for [people to choose Perch](https://grabaperch.com/vs/wordpress) over other CMS's.

## 5. Does the cost fit the budget?

I'm kind of glad to see this point low on the list. Of course the client will have a budget in mind for the site and you'll need to fit the cost of the CMS into that, but we're not limited to just the free CMS's on the market. Again, this is another reason why people end up using WordPress.

There are other options, though. I haven't tried it myself, but I've heard really good things about [Craft](https://craftcms.com/), which for a small price offers a very flexible and friendly user interface for clients to easily edit and add content.

![Craft's admin UI](/images/look-for-in-cms/craft-admin.jpg)

## 6. What platform is it built on?

I guess asking about the platform of the CMS is more related to what languages you are familiar with. If you know a decent amount of PHP then, again, WordPress is probably your best friend. Although, what other factors could steer you towards another underlying language?

Maybe the client has an API that's designed to be interacted with via node.js? It could even be a headless CMS, that needs to interact with several platforms all at once. An example of this would be [GatherContent](https://gathercontent.com/), as it has a [wide array of integrations](https://gathercontent.com/integrations) that allow you to connect with a range of CMS's and platforms.

## Why are we missing these points?

I _could_ make a few assumptions about these points that we might be making: we play it safe with our familiar choices; we won't spend money on something we can get for free; it doesn't fit the development stack etc. However, I won't go into this now.

What I will say is that we should open our minds to the CMS landscape. Take a look at the competition or other options you might think will work better for your client… **play the field a bit**. It might be the only chance you get. I certainly wish I had the time to try them all.

I hope you found this article useful. As I said above, feel free [to tweet me](https://twitter.com/daviddarnes) with your thoughts and share what you think it a good reason to try a different CMS.

:v:
