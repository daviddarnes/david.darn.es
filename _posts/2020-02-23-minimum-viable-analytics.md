---
title: "Minimum viable analytics"
excerpt: "I recently switched all of my personal project sites to [Netlify](https://netlify.com). I'd like to share how I made the move, my experiences, and the tooling I use to manage domains and track analytics."
icon: article
category: article
colour: "#0d26ca"
image: "/images/minimum-viable-analytics/minimum-viable-analytics-banner.png"
---

I recently switched all of my personal project sites to [Netlify](https://netlify.com). I'd like to share how I made the move, my experiences, and the tooling I use to manage domains and track analytics.

## Domains

Ever since I got into the hobby of domain hoarding I've used [Gandi.net](https://www.gandi.net/). It might not be the most popular, but I've had a great experience from the beginning. Reasonable pricing and fairly prompt customer support. Pretty wide selection of TLDs too.

## Netlify DNS

Up until now I've been managing my domains with [Cloudflare](https://www.cloudflare.com/), by adding Cloudflare nameservers to the Gandi admin. Cloudflare gave me more control over my domains as well as a selection of features from their free tier, one of which being Analytics. It was nice to see viewing stats, but it doesn't show specific URLs. I guess it's more for monitoring, not for someone who wants to know how well their blog post is doing.

![Cloudflare Analytics](/images/minimum-viable-analytics/cloudflare-analytics.png)

Another featured I used is the [Google Analytics 'App'](https://www.cloudflare.com/apps/googleanalytics) which linked with my Google account and in turn Google Analytics. It's a clever way to link your site up as it saves you adding analytics code to your codebase and environment variables.

However Google Analytics is too far over in the opposite direction. All the different views, metrics, filters are pretty overwhelming. Let's stop here though, I'll save my Google Analytics gripes for later on.

I found out [Netlify could manage my domains](https://docs.netlify.com/domains-https/netlify-dns/) by accident when I was configuring this site you're on now and [my main site](https://darn.es). Netlify offers both the ability to buy domains through them or manage domains in the same way Cloudflare does, by adding their nameservers to wherever you bought the domain from (Gandi in my case).

![Netlify DNS records example](/images/minimum-viable-analytics/netlify-dns.png)

I was already onboard with Netlify, and the idea of using them to manage my domain records sounded great. The most appealing feature is that you can actually see a Netlify site linked with a domain on their DNS service. Prior to this I was pointing Cloudflare to whatever hosting platform I was using and crossing my fingers until it worked. This new setup with Netlify feels much more cohesive.

## Netlify and Netlify Analytics

As mentioned at the top of this article, I've switched all my personal sites to Netlify. While I am a fan of their hosting, their Analytics feature I was super keen to try. It really bothered me that I had to use JavaScript running on someones computer to find out what they were doing on my sites. It's intrusive, heavy handed, detrimental to performance, and in some ways unreliable.

![Netlify Analytics](/images/minimum-viable-analytics/netlify-analytics.png)

[Netlify Analytics](https://www.netlify.com/products/analytics/) has a far more elegant approach of providing an interface to show URL stats from the server, which is data that is already there. Rather than asking for information from someones computer with JavaScript, like Google Analytics does, the server is making note of any URL requested. You also don't have to store cookies on the users client, like Google Analytics does, avoiding the need to add those pesky cookie banners.

![Netlify Analytics graph](/images/minimum-viable-analytics/minimum-viable-analytics-banner.png)

The two most satisfying parts of using Netlify Analytics for me has been the moment I turned it on I saw a month of historical stats appear immediately, and then seeing all the 404 errors from bots trying to hack a non-existent WordPress site.

![Netlify Analytics panel showing a list of URLs to non-existent WordPress files](/images/minimum-viable-analytics/netlify-analytics-not-found.png)

Interestingly, I posted a similar shot to above on Twitter and I was told that in the last couple of hours a serious vulnerability had been found in a WordPress plugin and [over 200,000 sites were at risk](https://twitter.com/ajeet_online/status/1229546973599977475). I've enabled this feature on a couple of my sites and I'll be using it to track some stats and hopefully action on them. It's a nice in-between the complexity of Google Analytics and the very high-level of Cloudflare Analytics.

## Google Search Console

Despite my negative opinion of Google Analytics, Google still does provide some useful tooling that can help with improving SEO and provide website stats. [Google Search Console](https://search.google.com/search-console/about) is Webmaster tools, if you used it in the past, and shares crawling info on your own websites. Rather than adding JavaScript, Search Console can be enabled by [adding a TXT record to your domain records](https://support.google.com/webmasters/answer/9008080#domain_name_verification). Again this is unobtrusive to your audience and only gives you information that Google has already captured when they crawl your site or when people use Google to find your site.

![Search Console](/images/minimum-viable-analytics/search-console.png)

There's a fair bit of data that can be found in Search Console. Top linked pages (also known as backlinks), top linking sites, what people search for before arriving on your site. Two features I often use is submitting URLs for indexing and submitting my sitemap. Google will queue these up for crawling and let you know if there are any errors.

## Further reading

I'm not saying my setup is the defacto way to manage domains and record analytics, but it works well for me and I think it works really well for my audience. Here's some helpful links if you want to achieve the same:
- [Pick a domain from Gandi.net](https://www.gandi.net/)
- [Changing nameservers on Gandi](https://docs.gandi.net/en/domain_names/common_operations/changing_nameservers.html#contents)
- [Deploying a Netlify site from git](https://www.youtube.com/watch?v=mN9oI98As_4)
- [Netlify DNS documentation](https://docs.netlify.com/domains-https/netlify-dns/)
- [Netlify Analytics documentation](https://docs.netlify.com/monitor-sites/analytics/)
- [About Google Search Console](https://support.google.com/webmasters/answer/9128668?hl=en)

✌️
