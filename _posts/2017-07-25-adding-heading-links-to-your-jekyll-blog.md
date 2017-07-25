---
title: "Adding heading links to your Jekyll blog"
icon: tutorial
colour: "#FA709A"
excerpt: "Just a brief JavaScript trick to get anchor links added to your Jekyll blog post headings"
---

I just spent the last hour or so fiddling around with my blog and portfolio. Both of them I thought could do with larger type to improve legibility and to give more of an impact.

After I increased the font size I increased the width of the main content. And then it dawned on me...

<< **look at this huge gap on the side of this blog!!**

Completely wasted space, just a really long line that merely adheres to my site style. This space should be put to more practical use.

Well one of the convient things Jekyll does out of the box is add `id` attrbiutes to headings generated with markdown in posts and pages. Which means that people can link to a specific section on a page, but the only way to get the id for the link is to instpect the page and find the heading id.

Wouldn't it be cool if there was a link next to the heading so you link people easily? :thinking:...

## How to add a heading link like the one next to this heading!

I realise this type of trick has been done a few times with ever so slightly different JavaScript, but here is my spin on the whole thing:

``` js
const headings = document.querySelectorAll('h2,h3'); // 1
const linkContent = '🔗'; // 2
for (const heading of headings) { // 3
    const linkIcon = document.createElement('a'); // 4
    linkIcon.setAttribute('href', `#${heading.id}`); // 5
    linkIcon.innerHTML = linkContent; // 6
    heading.appendChild(linkIcon); // 7
}
```

I've marked the above script with numbers, so going through each line we are:

1. Grab all the headings you want to link (h1 to h6)
2. A nice icon or piece of html for your link icon
3. For each heading in your group of headings...
4. Create an anchor element
5. Add the heading id as the anchor link
6. Add your icon or html to the anchor
7. Add it to the heading (appended after the heading text content)

I hope I've explained this well enough. I'm sure this script is quite trivial, but I always find it useful when people explain what the code is doing so you can either take it as is or manipulate it to your needs.

Now that space on the left of my blog posts isn't such a waste of space anymore.

Hope you find this useful. :v:
