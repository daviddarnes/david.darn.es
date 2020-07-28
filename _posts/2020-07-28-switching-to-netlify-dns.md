---
title: "Switching to Netlify DNS"
excerpt: "If you're onboard with [Netlify](https://netlify.com) then maybe you should switch your custom domains to their platform as well. In this tutorial I'll show you how to move your custom domain to Netlify DNS and how to link it with a project on Netlify."
icon: tutorial
category: tutorial
colour: "#1182a9"
image: "/images/netlify-dns/netlify-dns-banner.png"
---

**If you're onboard with [Netlify](https://netlify.com) then maybe you should switch your custom domains to their platform as well. In this tutorial I'll show you how to move your custom domain to Netlify DNS and how to link it with a project on Netlify.**

Domain management can be a real pain, to me at least anyway. I think it's down to the fact that I don't do it very often, and when I am doing it the terminology is slightly misleading or abstracted.

> Do I wan a `CNAME` or a an `A` record? What did I do last time??
>
> Dang, I forgot to redirect the `www` subdomain to the bare domain… 
>
> …how do I do that again???

A few of the questions that go through my brain when sorting out a new domain. If you're wondering where I buy my domains, I use [Gandi](https://gandi.link/f/e20f1f35) and have been for the last 11 years. **Use [this link to get 20% off a domain](https://gandi.link/f/e20f1f35) you buy with Gandi.**

To alleviate some of these pain points when managing domains I've been switching them over to [Netlify DNS](https://docs.netlify.com/domains-https/netlify-dns/). The following is a write up of how I've been switching my domains over, plus any gotchas I encountered along the way.

## Prerequisites

The following tutorial assumes you a custom domain ready to use, along with a project hosted on Netlify 👍. You'll also need to sort out any possible caching issues, this is to ensure domains resolve to their correct state when you load them in a browser.

One of the most common caching problems with domains is the TTL, the "Time To Live". A TTL is a numerical value representing the duration of time the server assumes a domain record value before checking again. For example, if the TTL on a domain record is `10800` then the server will not check this record value again for 10800 seconds or 3 hours for us humans. You can find out the TTL of a domain record by using the `dig` command in your CLI tool, `dig yourdomain.com` and hit enter.

It's recommended you reduce this value to as short as possible and waiting for the full original TTL to finish before going through the Netlify DNS transfer process. That way you'll see the actual results sooner. There's a [guide over on the Netlify community forum on how to update your TTL](https://community.netlify.com/t/support-guide-minimal-downtime-for-a-live-site-dns-migration/141) before switching.

## Getting started

Head on over to your Netlify dashboard and click on "Domains". [Here's direct link to the Domains UI](https://app.netlify.com/dns) if you're feeling lazy.

![Domains view in Netlify](/images/netlify-dns/add-domain-button.png)

Click on "Add or register a domain" and enter your domain into the "Domain" field. You can also buy a new custom domain from here too, if you're wanting to keep your stack of services to a minimum.

For people who already own their domain clicking "Verify" will respond with Netlify telling you that the domain already has an owner, which is hopefully you. Click "Yes, add domain".

_There are some TLDs that Netlify can't sell yet, such as `.es` domains. Even if you own the domain Netlify will respond with this message, so if you already own the domain ignore the message._

### Prepare DNS records

![Add DNS records view](/images/netlify-dns/add-records.png)

Before switching the domain over Netlify gives you the opportunity to add any custom records. If the domain is for an existing live project this will hopefully reduce any downtime during the switch.

Anyone who has used Cloudflare for their DNS may recall that when you add a domain they automatically guess the records by looking at the domain's existing records. It's a clever trick, and saves you entering the records yourself. Why doesn't Netlify do this? I believe this is by design, so they don't accidentally add records that will be overwritten when you add a project to a domain using their UI.

![Add DNS record dialog](/images/netlify-dns/add-record-dialog.png)

Use the DNS records interface to add your domain records. I very much appreciate the additional labels added to the fields here, helps me jog my memory on what needs to be entered. You may only be using the custom domain for a project, in which case you can skip this step.

### Add nameservers

The final step of adding your custom domain is adding the nameservers to your domain provider. Nameservers provide the server IP when a domain is requested, essentially the place where all your domain records are kept. Netlify will give you a set of nameservers that look like this:

``` txt
dns1.p05.nsone.net
dns2.p05.nsone.net
dns3.p05.nsone.net
dns4.p05.nsone.net
```

You'll need to take these and add them within the admin of your domain with your domain provider. Gandi has a guide [here in their docs on how to update nameservers](https://docs.gandi.net/en/domain_names/common_operations/changing_nameservers.html#switching-to-external-nameservers), otherwise you can [use the official Netlify DNS docs](https://docs.netlify.com/domains-https/netlify-dns/delegate-to-netlify/).

Adding these will effectively pass over control of the domain to the Netlify dashboard, allowing you to control the domain records from the same UI as your web projects.

To finish up, click "Done" in Netlify Domains to complete the onboarding steps.

## Add your domain to a Netlify project

Once the domain is all configured and resolved you'll be able to use it with a Netlify project. Head on over to a project, click on "Settings" and then "Domain management" in the sidebar.

![Add custom domain section in Netlity project](/images/netlify-dns/add-custom-domain.png)

If you click "Add custom domain" you'll be presented with a similar custom domain field you saw in the domain set up process. You can add a bare domain or a subdomain.

Add your custom domain, whether it's the root domain or subdomain, and click "Verify". Click on "Yes, add domain" and boom, [it's done](https://twitter.com/cassidoo/status/1285616015620046849)!

## Fine tuning and gotchas

At this point of the tutorial I'd probably be showing you how to set up a record for redirecting the `www` subdomain to your bare domain, but if you use a bare domain in a project Netlify it will automatically create the record ✨

You do also have full control over your domain records too, letting you point domains to external platforms or records for verification purposes or whatever you need.

This isn't required, but you may want to ensure that your custom domain is the defacto address for your site by redirecting your Netlify app subdomain. Redirecting it can be done by adding the following to a file called `_redirects` to the root of your project:

```
http://myproject.netlify.app/* http://myproject.com/:splat 301!
https://myproject.netlify.app/* https://myproject.com/:splat 301!
```

Note that you'll need to replace the URLs with your actual Netlify subdomain and custom domain.

### Removing records

The only gotcha I encountered during this process was around removing records. When you add a custom domain to a project a `NETLIFY` record is automatically created, which under the hood is actually an `A` record. These records can only be controlled via the the project that created them, and at present can't be removed. This isn't entirely an issue, as if the domain is removed from the project a "Not found" error is returned instead.

If you really want the record removed then [get in touch with the Netlify support team](https://community.netlify.com/) and they'll help you from there.

## Rounding up

If you're facing problems it's always worth checking out the [official Netlify docs](https://docs.netlify.com/domains-https/custom-domains/) and [surfing the community forum](https://community.netlify.com/) for further guidance.

I do like the experience that Netlify has created around domains, however I am a little biased as I use them for most of my web projects. I think the interface and experience is a little rough round the edges, but I expect this to only get smoother and more elegant over time.

Regardless, having my web projects and domain management in one place really plays into my organisational mind. I hope you found this guide helpful, if you did feel free to give it a share.

✌️
