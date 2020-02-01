---
title: "Page translations and multi-language selects"
excerpt: "Multi-language sites are straight up hard to do. You would think there's standard HTML spec stuff to handle this kinda stuff? Well there is!"
icon: tutorial
category: tutorial
colour: "#23a1a6"
image: "/images/multi-language/multi-language-banner.png"
---

Multi-language sites are straight up hard to do. You can automate, plugin and redirect all you like but you'll still be left with the reality that you're going to be dealing with multiple instances of the same "thing". I've worked on multi-language sites before, back in my WordPress saga days, and it sure got complicated.

You would think there's standard HTML spec stuff to handle this kinda stuff? Well there is! I've recently been expanding [our catalog of tutorials for Ghost](https://ghost.org/tutorials/) and one of them was a guide on [using multiple languages in Ghost](https://ghost.org/tutorials/multi-language-content/). While working on this [Kym](https://kymellis.co/) from the team enlightened me on `<link>` elements that denote alternate versions of the same page.

```html
<link rel="alternate" href="http://mobile.example.com/" />
```

This `<link>` element would reside within the `<head>` element of the page. I guess it acts a bit like `canonical` but not to the extent of saying "this is the original". [Examples can be found on microformats.org](http://microformats.org/wiki/rel-alternate).

## Using `rel="alternate"` with translations

So what can this attribute (and value) do to help our multi-language pain points? When the `rel="alternate"` attribute is used in conjunction with the `hreflang=""` attribute it can denote translated versions of the currently viewed page.

```html
<head>
  <title>My web page in english</title>
  <link rel="alternate" href="http://example.com/fr/" hreflang="fr" />
  <link rel="alternate" href="http://example.com/de/" hreflang="de" />
</head>
```

Search engines like Google will index the pages along with the translated counterparts that have been referenced with the `<link>` element. There's a bit more info [here on this Google Support page](https://support.google.com/webmasters/answer/189077). Google will then serve the user whichever page is right for them depending on their region, using the `hreflang` value as a reference.

Further details on applying this kind of meta information to your web pages can be found in the [Moz learning resources](https://moz.com/learn/seo/hreflang-tag). Additionally Nomensa have covered these attributes as well as other microformats for [creating accessible multi-lingual sites](https://www.nomensa.com/blog/2010/7-tips-for-multi-lingual-website-accessibility).

## Building a language select dropdown

Let's circle back to the original point of this tutorial, creating a language select. I've approached this in the same fashion as I do with most interactions, I'm using JavaScript to enhance what already exists on the page.

In this instance I'm using the existing `<link>` elements that state the alternate translations for the page to generate a list of links that will take the user to another translation of that page. Rather than give a full break down of the code I've provided an annotated version below. If you're looking for a version without the comments you can [check out this CodePen](https://codepen.io/daviddarnes/pen/QWwzePz?editors=1010).

```html
<!--
details element placed on the page,
ready to be populated by the JavaScript
-->
<details data-language-select></details>
```

```javascript
// Grab the details element that will be the language select
const langSelect = document.querySelector("details[data-language-select]");

// Grab all the alternate translations as an array
const translations = [...document.querySelectorAll("head [hreflang]")];

// Check if both select and translations exist
if (langSelect && translations.length) {
  // Generate the following HTML into the details element:
  // 1. <summary> title of the current language
  // 2. An unordered list of translations as links with a label and hreflang attribute
  langSelect.innerHTML = `
      <summary>Language: ${document.documentElement.lang}</summary>
      <ul>
        ${translations
          .map(link => {
            return `<li><a href="${link.href}" hreflang="${link.hreflang}">${link.hreflang}</a></li>`;
          })
          .join("")}
      </ul>
    `;
}
```

One thing I should note is that the above assumes you've set a `lang=""` attribute on the `<html>` element, which you should definitely do so users know what language the content they're looking at is in.

## Conclusion

What I really like about this method is that if feels like "the right way". We're using standard methods of marking our content and our translated versions alongside them.

We're also not trying to be clever. I worked way too hard in trying to automate translations on those WordPress sites. There's a reason professional translators exist. The same subject is covered, amongst others, here in [this Tuts+ article on building a multi-lingual site](https://webdesign.tutsplus.com/articles/tips-for-designing-and-building-a-multilingual-website--cms-24708). Translate your content when you can get a professional to take a look at them and add those `<link>` elements in later.

Let me know your thoughts [on Twitter](https://twitter.com/DavidDarnes/), and give this article a share. Thanks for reading ✌️
