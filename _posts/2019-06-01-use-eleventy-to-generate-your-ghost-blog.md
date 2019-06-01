---
title: "Use Eleventy To Generate your Ghost Blog"
excerpt: "Last night I had a thought: What if I could just source my blog posts from the [Ghost Content API](https://docs.ghost.org/api/content/) and then generate a static blog all inside of [Eleventy](https://www.11ty.io/)?"
icon: tutorial
colour: "#55c3ff"
---

**Eleventy is swiftly becoming the most popular static site generator within my online feeds. [Check out the site](https://www.11ty.io/) if you want to know more, if you're a fan of Jekyll then you'll probably like Eleventy just as much (maybe more).**

Last night I had a thought, which was only perpetuated by [Andy](https://mobile.twitter.com/andybelldesign/status/1134565751074037774):

> What if I could just source my blog posts from the [Ghost Content API](https://docs.ghost.org/api/content/) and then generate a static blog all inside of Eleventy?

## Preface
You're going to need Eleventy installed for this in some shape or form, [check out the docs](https://www.11ty.io/docs/) to get setup.

## Data sourcing
Creating and getting data in Eleventy builds upon the method that Jekyll already has. A `_data/` directory is where you can store chunks of data that are then exposed in your template files. [Eleventy takes this one step further though](https://www.11ty.io/docs/data/), with the ability to use JavaScript files to source and create data structures.

I guess if we can use JavaScript then we can probably use some libraries too? Let's have a go by installing the [Ghost Content API Client Library](https://docs.ghost.org/api/javascript/):

``` bash
npm install @tryghost/content-api --save-dev
```

Then a data file, in this case the file is called `_data/posts.js`:
``` js
// The library that was just installed
const contentAPI = require('@tryghost/content-api');

// New instance with Ghost demo API credentials
const api = new contentAPI({
  url: 'https://demo.ghost.io',
  key: '22444f78447824223cefc48062',
  version: 'v2'
});

// Export data called from the API
module.exports = async function() {
  return api.posts.browse()
      .catch((err) => {
          console.error(err);
      });
}
```

## Templating
This clever API code is all well and good, but you're not going to see anything without some template files to present content. Below I've provided a very raw example using nunjucks templating, called `index.njk`. Note that the variable `posts` is the same as the name given to the data file, this is part of how Eleventy passes that data to the template files:

``` html
<ul>
  {% raw %}{% for post in posts %}
    <li>
       <a href="/posts/{{ post.slug }}/">
         {{ post.title }}
       </a>
    </li>
  {% endfor %}{% endraw %}
</ul>
```

Let's run Eleventy with `eleventy serve` and see what happens:

![Unformatted list of linked post titles](/images/eleventy-ghost-blog/post-list.png)

What a beautifully designed blog :nail_care:. Joking aside, it worked! We sourced content directly from the Ghost API and generated a little static blog with Eleventy! :guitar:

## Rendering single posts
This blog isn't quite a blog though, we're linking each post to an optimistic, but disappointing, 404 page. I guess we could link to the original post on a Ghost site, but that's not a real static blog right?

Oddly this part of my personal challenge was what I got stuck on the most. The creation of single pages for chunks of content is [wrapped up in 'Pagination'](https://www.11ty.io/docs/pagination/#paging-an-object). Which on the face of it sounds weird. Why would I want to use pagination, something that creates groups of things, to create the one thing.

If you think about it though it's not that far off. Pagination is where you split a long array of items into smaller chunks. Well what if you wanted to split those chunks to a small enough size that each page was just 1 thing? That's pretty much what we want, a single page with one item on each.

Again, we're going to use nunjucks for templating, but enlist some frontmatter to configure our pagination:

``` html
{%- raw %}
---
pagination:
  data: posts
  size: 1
  alias: post
permalink: posts/{{ post.slug }}/
---
<h1>{{ post.title }}</h1>
{{ post.html | safe }}{% endraw %}
```

Let's break it down.
- We're using the `pagination` option
- The `data` we want to use is `posts`
- The `size` of the pagination chunk is just `1` post
- Providing an `alias` key name called `post`, better to deal with the singular in this context rather than a plural key
- Finally the `permalink` option it to tell Eleventy to output each post to a path matching the post slug.

I've called this file `post.njk` but since it's never outputted then it doesn't really matter.

![All the post files generated, as well as the project files](/images/eleventy-ghost-blog/file-directory.png)

![Example post in the browser](/images/eleventy-ghost-blog/example-post.png)

We're done! An Eleventy static site sourcing content from the Ghost API.

This doesn't just work for the Ghost API, with the JavaScript fetch API we can pull in content from all sorts of places.

How about all your repos on GitHub?
``` js
const fetch = require("node-fetch");

module.exports = async function() {
  const data = await fetch('https://api.github.com/users/daviddarnes/repos');
  const json = await data.json().then(data => data);
  return json;
};
```

This feature alone makes Eleventy a really powerful tool. Have a play and [let me know what you make with it](https://twitter.com/daviddarnes).
