---
title: "How to use Ghost with Jekyll"
excerpt: "Someone made an interesting query recently that I couldn't help but take on as a challenge: Is there any way to use [Ghost](https://ghost.org) with [Jekyll](https://jekyllrb.com)?"
icon: tutorial
category: tutorial
colour: "#ca7600"
image: "/images/ghost-jekyll/ghost-jekyll-banner.png"
---


**Someone made an interesting query recently that I couldn't help but take on as a challenge: Is there any way to use [Ghost](https://ghost.org) with [Jekyll](https://jekyllrb.com)? Turns out there is, and for those that want to cut to the code [here's a handy gist](https://gist.github.com/daviddarnes/eb956c1a8b57f4249ea57516b06ca89e).**

I recently released a starter for using a [Ghost](https://ghost.org) site with the static site generator [Eleventy](https://11ty.io), check it out the [starter if you're interested](https://github.com/TryGhost/eleventy-starter-ghost/). I also wrote up about it [on the Ghost blog](https://ghost.org/blog/eleventy/), which includes links to the Ghost docs on how to use Eleventy with Ghost.

## Set the scene

The relevancy of Jekyll to Eleventy? Well when we tweeted out the Eleventy post [Mathias Aggerbo](https://twitter.com/maggerbo) asked this:
> Are there any way to use Ghost with Jekyll?
>
> – <cite><a href="https://twitter.com/maggerbo/status/1159097416324440064">Mathias Aggerbo</a></cite>
{:cite="https://twitter.com/maggerbo/status/1159097416324440064"}

For those of you who know me fairly well you'll know that Jekyll [is](https://www.siteleaf.com/blog/making-your-first-jekyll-theme-part-1/) [close](https://david.darn.es/2017/07/25/adding-heading-links-to-your-jekyll-blog/) [to](https://webdesign.tutsplus.com/tutorials/how-to-create-and-publish-a-jekyll-theme-gem--cms-27475) [my](https://david.darn.es/2016/05/17/jekyll-conf-lightning-talk/) [heart](https://alembic.darn.es/), so I was keen to help find a solution.

But how? In my experience Jekyll isn't known for working with APIs. Jekyll is designed as the more typical flat file CMS, taking text files (typically [markdown files](https://jekyllrb.com/docs/step-by-step/08-blogging/)) and turning them into html files. Once more it's Ruby based, so JavaScript API libraries aren't going to be the smoothest things to plug in.

Enter stage right [Phil Hawksworth](https://twitter.com/philhawksworth):
> A pattern I’ve used for a lot with a variety of SSGs is to have something like Gulp run the build. It pulls data from APIs, stashes it in the data files the SSG prefers, then generates the site with the SSG.
>
> This can keep your options open so you can choose the tool you prefer.
>
> – <cite><a href="https://twitter.com/philhawksworth/status/1159193504851144705">Phil Hawksworth</a></cite>
{:cite="https://twitter.com/philhawksworth/status/1159193504851144705"}

[gulp.js](https://gulpjs.com/) is a great tool, I often forget how useful and versatile it can be. The homepage text sums up gulp.js pretty well:

> gulp is a toolkit for automating painful or time-consuming tasks in your development workflow, so you can stop messing around and build something
>
> <cite>– <a href="https://gulpjs.com">Gulp website</a></cite>
{:cite="https://gulpjs.com/"}


It's designed to be used in the command line, as [gulp tasks](https://gulpjs.com/docs/en/getting-started/creating-tasks). For example, I could create a task called `styles` that turns a `.scss` file into a `.css` file, minifies that file and then clones it into my production directory. All by a running a single single command, `gulp styles`. Very handy if you want to make custom file processing workflows and already have some familiarity with Node / JavaScript.

## Coding

Right, so we have our base components to achieve a link between Ghost and a Jekyll site:
1. [Ghost](https://ghost.org): Where our content will be sourced from
1. [Ghost Content API Library](https://ghost.org/docs/api/v2/javascript/): How we're going to get the content
1. [gulp.js](https://gulpjs.com): How we're going to take that content and produce markdown files for Jekyll to consume

Because we're using gulp.js all the following code is inside a single `gulpfile.js`. If you're a bit unfamiliar with gulp I'd recommend checking out the [gulp.js documentation](https://gulpjs.com/docs/en/getting-started/quick-start) on how to get started and it's concepts.

### Source content via API

The [JavaScript Client Library](https://www.npmjs.com/package/@tryghost/content-api) for Ghost makes this a fairly clean process. I'm just using the demo API configuration so you'll need to replace this with the credentials of the Ghost site, more info on [how to get those credentials can be found here](https://ghost.org/docs/api/v2/javascript/content/#authentication).

In a `gulpfile.js`:

``` js
const gulp = require("gulp");
const ghostContentAPI = require("@tryghost/content-api");

// Create API instance with Ghost credentials
const api = new ghostContentAPI({
  url: 'https://demo.ghost.io',
  key: '22444f78447824223cefc48062',
  version: "v2"
});

gulp.task('ghost', async function() {

  // Use API to get all posts
  // with their tag and author information
  const posts = await api.posts
  .browse({
    include: "tags,authors",
    limit: "all"
  })
  .catch(err => {
    console.error(err);
  });

  // ...

});
```

### Construct an array of files

We've got our API data, but we want to loop through that data and produce files from each post item. Out of the box gulp is designed to take "file A" and turn it into "file B". We'll need to bring in some dependencies that will allow us to turn data into files.

Here's what I ended up using:
- [streamArray](https://www.npmjs.com/package/stream-array): Taking the array of `posts` we've created and feeding that into Node
- [Vinyl](https://www.npmjs.com/package/vinyl): A library created by the gulp.js team for creating files within a gulp.js task

``` js
const streamArray = require('stream-array');
const File = require('vinyl');

// gulp.task('ghost'...

  // Iterate over posts
  const files = posts.map(post => {

    // Getting some values from the post object
    const { published_at, slug, title } = post;

    // Take a single post and create a new file
    return new File({

      // Name the file based on the post date
      // and the slug
      path: `${published_at.slice(0,10)}-${slug}.md`,

      // Write the title of the post
      // inside the file
      contents: Buffer.from(title)
    });
  });

  // Stream the array of file instances into Node
  return streamArray(files)

    // Put the files in a '_posts' directory
    .pipe(gulp.dest('./_posts'));
});
```

I've done my best to explain it in the comments. Note that we're using the published date and slug of each post to construct the filename and placing them in a `/_posts` directory, which follows [Jekyll's post filename format](https://jekyllrb.com/docs/posts/#creating-posts). The `.slice(0,10)` is to remove the time from the full date string.

### Create frontmatter and markdown

The final part to this `gulpfile.js` task is taking the Ghost post data and formatting it in such a way that Jekyll will read it as a typical markdown post. Again, dependencies to the rescue!

Here we're using template strings to construct the format of our markdown files, and then use [handlebars](https://www.npmjs.com/package/handlebars) to transform the variables into the values we want. We could just use regular JavaScript to put the data straight into the template, but this a bit easier to read and could be extended upon without overly complex template strings.

``` js
{%- raw -%}
const Handlebars = require('handlebars');

// Create markdown template
// using handlebars templating
// (No indentation so it doesn't appear in the file)
const template = `
---
title: {{ title }}
excerpt: {{{ excerpt }}}
feature_image: {{ feature_image }}
tags:
{{#each tags}}
- {{ this.slug }}
{{/each}}
---
{{{ html }}}
`;

// Create a compiler function
// with the library and template string
const templateFunction = Handlebars.compile(template.trim());

// gulp.task('ghost'...

      // Pass the post to the template function and
      // in turn pass it to the content of the file
      contents: Buffer.from(templateFunction(post))
    });
  });

  // streamArray...
{% endraw %}
```

Another plus to using handlebars here is that it mirrors the [Liquid templating](https://shopify.github.io/liquid/) language used in Jekyll, so anyone familiar with working on the project may have an easier time making edits and additions.

The template string I've used is more of an example, just exposing things like `title`, `tags`, `html` (the main content) etc. If you want to expose more of the Ghost API to your Jekyll site, like post attributes and other endpoints, you can [check out the Ghost docs](https://ghost.org/docs/api/v2/content/#endpoints).

## All together now!

<script src="https://gist.github.com/daviddarnes/eb956c1a8b57f4249ea57516b06ca89e.js?file=gulpfile.js"></script>

If you [click through to the gist](https://gist.github.com/daviddarnes/eb956c1a8b57f4249ea57516b06ca89e) you'll see that I've added a `package.json` that you can easily copy too.

Pretty nifty method of bringing Ghost and Jekyll together I think. Feel free to [chat with me on Twitter](https://twitter.com/DavidDarnes) if you've got some improvements or are using this yourself!

PS. Thanks to [Phil](https://twitter.com/philhawksworth) for giving me the inspiration, and thanks to [egg](https://twitter.com/allouis_) for the refactoring and code review
