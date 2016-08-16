---
title: I Put CSS in My HTML and Nothing Exploded
colour: "#84217c"
icon: article
image: https://david.darn.es/images/css-in-my-html/inline-css-header.jpg
---

**When I first felt comfortable with front-end web development, I thought inline CSS was a filthy thing to do; something that could only be done in haste or from poor implementation. Thankfully, I'm a little wiser now and can understand that there is almost _always_ a reason behind the implementation.**

<!-- more -->

In this article, I'm going to take a look at a few of the possible negatives of inline CSS and "Internal Stylesheets", along with an example of practical usage. Let's take look at some of the reasons why people might be adverse to placing their styles inline.

### It's difficult to manage

The tooling we have today means that it's pretty darn easy to plant CSS directly onto the page with a `<style>` block, or even directly applied to the element. 🛠

### It loads unwanted CSS

It depends 🌈. If you're working on a small site like mine, the amount of unwanted CSS is not worth considering. However, for large scale sites and applications, you might want to look into other tooling.

### You can't depend on JavaScript for CSS

You can, if your application depends on JavaScript. There are some cases where non-JavaScript users should be catered for. However, there are also cases where applications and sites with heavy dependance on JS should just go with the flow. 🌊

### I can't read the source

Eh? Why are you reading the source so intently? Stay in the web inspector - it's all cool there. 🔬

## The practical test

So, with all that in mind, let's take this into a practical scenario. Now, this scenario isn't an app or large scale website - it's just this blog - but it is taking into account all the items above! In this example, I've taken the CSS for this site and added it directly into the `<head>` as an "internal stylesheet", which is technically not inline, but some people might consider it like that. I'll cut to the chase and give the results:

### Using an external linked `.css` file 

- Mobile friendliness: **100/100**
- Mobile speed: **89/100**
- Desktop speed: **96/100**

_Results from [testmysite.thinkwithgoogle.com](https://testmysite.thinkwithgoogle.com/)_

- PageSpeed Score: **A, 96%**
- YSlow Score: **A, 95%**
- Page Load Time: **0.7s**
- Total Page Size: **116kb**

_Results from [https://gtmetrix.com/](https://gtmetrix.com/)_

### Using an internal stylesheet with `<style>`

- Mobile friendlyness: **100/100**
- Mobile speed: **98/100**
- Desktop speed: **98/100**

_Results from [testmysite.thinkwithgoogle.com](https://testmysite.thinkwithgoogle.com/)_

- PageSpeed Score: **A, 97%**
- YSlow Score: **A, 96%**
- Page Load Time: **0.5s**
- Total Page Size: **116kb**

_Results from [gtmetrix.com](https://gtmetrix.com/)_

![Google speed results](https://david.darn.es/images/css-in-my-html/results.png)

## Conclusion

Awesome! My site loads faster **(from 0.7s to 0.5s)** and I'm getting perf points from Google, which in reality mean nothing, but at least my site is seen more quickly on devices with poor connections. So, what am I trying to say here? I'm not demanding you go off and make all your CSS inline right now. I'm saying: consider the options, weigh them up against the norm and test them out. As long as you have a good reason behind the implementation, it kind of doesn't matter what others think. ✌️
