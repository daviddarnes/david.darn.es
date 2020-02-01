---
title: "Page translations and multi-language selects"
excerpt: "Multi-language sites are straight up hard to do. You would think there's standard HTML spec stuff to handle this kinda stuff? Well there is!"
icon: tutorial
category: tutorial
colour: "#23a1a6"
image: "/images/multi-language/multi-language-banner.png"
---

Multi-language sites are straight up hard to do. You can automate, plugin and redirect all you like, but you'll still be left with the reality that you'll be dealing with multiple instances of the same thing. I've worked on multi-language sites before, back in my WordPress saga days, and it sure got complicated.

You would think there's standard HTML spec thingers to handle this kinda stuff? Well, there is! I've recently been expanding [our catalog of tutorials for Ghost](https://ghost.org/tutorials/) and one of them was a guide on [using multiple languages in Ghost](https://ghost.org/tutorials/multi-language-content/). While working on this, [Kym](https://kymellis.co/) from the team enlightened me about `<link>` elements that denote alternate versions of the same page.

```html
<link rel="alternate" href="https://mirror.site.com/" />
```

This `<link>` element would reside within the `<head>` element of the page. I guess it acts a bit like `canonical`, but not to the extent of saying "this is the original". [Examples can be found on microformats.org](http://microformats.org/wiki/rel-alternate).

## Using `rel="alternate"` with translations

So, what can this attribute (and value) do to help our multi-language pain points? When the `rel="alternate"` attribute is used in conjunction with the `hreflang=""` attribute, it can denote translated versions of the currently viewed page.

```html
<title>My web page in english</title>
<link rel="alternate" href="https://site.com/fr/" hreflang="fr" />
<link rel="alternate" href="https://site.com/de/" hreflang="de" />
```

Search engines, like Google, will index the pages, along with the translated counterparts that've been referenced with the `<link>` element. There's a bit [more info here on this Google Support page](https://support.google.com/webmasters/answer/189077). Google will then serve the user whatever page is right for them, depending on their region, using the `hreflang` value as a reference.

Further details on applying this kind of meta information to your web pages can be found in the [Moz learning resources](https://moz.com/learn/seo/hreflang-tag). Additionally, Nomensa have covered these attributes, as well as other microformats for [creating accessible multi-lingual sites](https://www.nomensa.com/blog/2010/7-tips-for-multi-lingual-website-accessibility).

## Building a language select dropdown

Let's circle back to the original point of this tutorial: creating a language select. I've approached this in the same fashion I do most interactions - I'm using JavaScript to enhance what already exists on the page.

In this instance, I'm using the existing `<link>` elements that state the alternate translations for the page to generate a list of links that'll take the user to another translation of that page. Rather than give a full breakdown of the code, I've provided an annotated version below. [Check out this CodePen](https://codepen.io/daviddarnes/pen/QWwzePz?editors=1010) to see everything in action, including an accessible method of toggling the language select (thanks [Andy Bell](https://hankchizljaw.com/wrote/a-progressive-disclosure-component/)).

```html
<head>
  <link rel="alternate" hreflang="fr" href="https://site.com/fr/" />
  <link rel="alternate" hreflang="jp" href="https://site.com/jp/" />
  <link rel="alternate" hreflang="de" href="https://site.com/de/" />
</head>
<!-- Details element in markup, ready for JavaScript -->
<div data-language-select></div>
```

```javascript
// Grab the details element that will be the language select
const langSelect = document.querySelector("[data-language-select]");

// Grab all the alternate translations as an array
const translations = [...document.querySelectorAll("head [hreflang]")];

// Check if both select and translations exist
if (langSelect && translations.length) {
  // Build a list of anchors from the translations
  const links = translations
    .map(link => {
      return `
      <li>
        <a href="${link.href}" hreflang="${link.hreflang}">${link.hreflang}</a>
      </li>
    `;
    })
    .join("");

  // Insert a summary showing the current language
  // and insert the links into a unordered list
  langSelect.innerHTML = `
    <button type="button" aria-expanded="false">Language: ${document.documentElement.lang}</button>
    <ul>${links}</ul>
  `;
}
```

One thing I should note is that the above assumes you've set a `lang=""` attribute on the `<html>` element, which you should definitely do so users know what language the content is in.

## Conclusion

What I really like about this method is that if feels like the 'right way'. We're using standard methods of marking our content and our translated versions alongside them.

We're also not trying to be clever. I worked way too hard in trying to automate translations on those WordPress sites; there's a reason professional translators exist. The same subject is covered, amongst others, here in [this Tuts+ article on building a multi-lingual site](https://webdesign.tutsplus.com/articles/tips-for-designing-and-building-a-multilingual-website--cms-24708). Get a professional to translate your content and when it's done, add the `<link>` elements in later.

Let me know your thoughts [on Twitter](https://twitter.com/DavidDarnes/). If you're feeling kind, give this article a share. Thanks for reading ✌️
