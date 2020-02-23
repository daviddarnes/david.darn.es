---
title: "Minimum viable analytics"
excerpt: "I recently switched all my personal project sites to [Netlify](https://netlify.com). I'd like to share how I made the move, my experiences, and the tooling I use to manage domains and track analytics."
icon: article
category: article
colour: "#0d26ca"
image: "/images/minimum-viable-analytics/minimum-viable-analytics-banner.png"
---

I recently switched all my personal project sites to [Netlify](https://netlify.com). I'd like to share how I made the move, my experiences, and the tooling I use to manage domains and track analytics.

## Domains

Ever since I got into the hobby of domain hoarding, I've used [Gandi.net](https://www.gandi.net/). It might not be the most popular hosting platform, but I've had a great experience with it from the beginning: reasonable pricing and fairly prompt customer support, with a pretty wide selection of TLDs, too.

## Netlify DNS

Up until now, I've been managing my domains with [Cloudflare](https://www.cloudflare.com/), adding Cloudflare nameservers to the Gandi admin. Cloudflare gave me more control over my domains, including a selection of features from their free tier, such as Analytics. This feature was nice to enable you to see viewing stats, but it doesn't show metrics for specific URLs. I guess it's more for monitoring overall traffic, rather than for finding out how well a particular blog post is doing.

![Cloudflare Analytics](/images/minimum-viable-analytics/cloudflare-analytics.png)

Another feature I used is the [Google Analytics 'App'](https://www.cloudflare.com/apps/googleanalytics), which links directly with Google Analytics. It's a clever way to add your site to Google Analytics, as it saves you adding their analytics code to your codebase and environment variables. However, Google Analytics is a step too far in the wrong direction - all the different views, metrics, filters are pretty overwhelming. Let's leave that thought here, though; I'll save my Google Analytics gripes for later on.

I found out [Netlify could manage my domains](https://docs.netlify.com/domains-https/netlify-dns/) by accident when I was configuring [my main site](https://darn.es) and the site you're on now. Netlify offers both the ability to buy domains through them or manage domains in the same way Cloudflare does, through adding their nameservers to whatever platform you bought the domain (in my case, Gandi).

![Netlify DNS records example](/images/minimum-viable-analytics/netlify-dns.png)

I was already onboard with Netlify and the idea of using their platform to manage my domain records sounded great. The most appealing feature is that you can actually see a Netlify site linked with a domain on their DNS service. Prior to this, I pointed Cloudflare to whatever hosting platform I was using and crossed my fingers until it worked. This new setup with Netlify feels much more cohesive.

## Netlify and Netlify Analytics

As mentioned at the top of this article, I'm now hosting my personal sites on Netlify. While I was already a fan of their hosting, the analytics feature has become the most appealing thing to try out. 

When using Google Analytics, it really bothered me that it requires you to use JavaScript on the client to find out what pages are being viewed. It's intrusive, heavy handed, detrimental to performance, and in some ways, unreliable.

![Netlify Analytics](/images/minimum-viable-analytics/netlify-analytics.png)

[Netlify Analytics](https://www.netlify.com/products/analytics/) has a far more elegant approach: it tracks page requests on the server, which is data that is already there. Rather than asking for information from someone's computer with JavaScript, like Google Analytics does, the server makes a note of any URL requested. You also don't have to store cookies on the user's client - again, like Google Analytics does - avoiding the need to add those pesky 'cookies' banners.

![Netlify Analytics graph](/images/minimum-viable-analytics/minimum-viable-analytics-banner.png)

The two most satisfying parts of using Netlify Analytics for me so far are the moment I turned it on, I saw a month of historical stats appear immediately, and then discovering all the 404 errors from bots trying to hack a non-existent WordPress site.

![Netlify Analytics panel showing a list of URLs to non-existent WordPress files](/images/minimum-viable-analytics/netlify-analytics-not-found.png)

Interestingly, I posted a similar shot to the above on Twitter and was told that in the last couple of hours, a serious vulnerability had been found in a WordPress plugin, where [over 200,000 sites were at risk](https://twitter.com/ajeet_online/status/1229546973599977475). I've now enabled this feature on a couple of my sites and will be using it to track some stats to hopefully action them. Netlify Analytics is a nice in between, with the complexity shown in Google Analytics and the very high-level view in Cloudflare Analytics.

## Google Search Console

Despite my negative opinion of Google Analytics, Google still does provide some useful tooling for SEO and Analytics. [Google Search Console](https://search.google.com/search-console/about), previously known as Webmaster Tools, shares crawling info on your sites. Rather than adding JavaScript, Search Console can be enabled by [adding a TXT record to your domain records](https://support.google.com/webmasters/answer/9008080#domain_name_verification). Again, this is unobtrusive to your audience and only gives you information that Google has already captured when they crawl your site, or when people use Google to find it.

![Search Console](/images/minimum-viable-analytics/search-console.png)

There's a fair bit of data that can be found in Search Console: top linked pages (also known as 'backlinks'), top linking sites, and what people search for before arriving on your site. Two features I often use are submitting URLs for indexing and submitting my sitemap. Google will queue these up for crawling and let you know if there are any errors.

## Further reading

I'm not saying my setup is the defacto way to manage domains and record analytics, but it works well for me and I think it will work really well for my audience. Here are some helpful links if you want to achieve the same results:
- [Pick a domain from Gandi.net](https://www.gandi.net/)
- [Changing nameservers on Gandi](https://docs.gandi.net/en/domain_names/common_operations/changing_nameservers.html#contents)
- [Deploying a Netlify site from git](https://www.youtube.com/watch?v=mN9oI98As_4)
- [Netlify DNS documentation](https://docs.netlify.com/domains-https/netlify-dns/)
- [Netlify Analytics documentation](https://docs.netlify.com/monitor-sites/analytics/)
- [About Google Search Console](https://support.google.com/webmasters/answer/9128668?hl=en)

✌️
