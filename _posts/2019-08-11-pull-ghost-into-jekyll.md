---
title: "Pull Ghost Into Jekyll"
excerpt: "Someone made an interesting query recently that I couldn't help but take on as a challenge: Is there any way to use [Ghost](https://ghost.org) with [Jekyll](https://jekyllrb.com)?"
icon: tutorial
category: tutorial
colour: "#ca7600"
---

**Someone made an interesting query recently that I couldn't help but take on as a challenge: Is there any way to use [Ghost](https://ghost.org) with [Jekyll](https://jekyllrb.com)? Turns out there is, and for those that want to cut to the code [here's a handy gist](https://gist.github.com/daviddarnes/eb956c1a8b57f4249ea57516b06ca89e).**

I recently released a Starter for using a [Ghost](https://ghost.org) site with the static site generator [Eleventy](https://11ty.io), check it out the [starter if you're interested](https://github.com/TryGhost/eleventy-starter-ghost/). I also wrote up about it [on the Ghost blog](https://ghost.org/blog/eleventy/), which includes links to the Ghost docs on how to use Eleventy with Ghost.

## Set the scene

The relevancy to this? Well when I tweeted this out [Mathias Aggerbo](https://twitter.com/maggerbo) asked this:
> Are there any way to use Ghost with Jekyll?
>
> – <cite>Mathias Aggerbo</cite>
{:cite="https://twitter.com/maggerbo/status/1159097416324440064"}

For those of you who know me fairly well you'll know that Jekyll [is](https://www.siteleaf.com/blog/making-your-first-jekyll-theme-part-1/) [close](https://david.darn.es/2017/07/25/adding-heading-links-to-your-jekyll-blog/) [to](https://webdesign.tutsplus.com/tutorials/how-to-create-and-publish-a-jekyll-theme-gem--cms-27475) [my](https://david.darn.es/2016/05/17/jekyll-conf-lightning-talk/) [heart](https://alembic.darn.es/), so I was keen to help find a solution.

But how? In my experience Jekyll isn't known for working with APIs. Jekyll is designed as the more typical flat file CMS, taking text files (typically [markdown files](https://jekyllrb.com/docs/step-by-step/08-blogging/)) and turning them into pages. Once more is't Ruby based, so JavaScript API libraries aren't going to be the smoothest things to plug in.

Enter stage left [Phil Hawksworth](https://twitter.com/philhawksworth):
> A pattern I’ve used for a lot with a variety of SSGs is to have something like Gulp run the build. It pulls data from APIs, stashes it in the data files the SSG prefers, then generates the site with the SSG.
>
> This can keep your options open so you can choose the tool you prefer.
>
> – <cite>Phil Hawksworth</cite>
{:cite="https://twitter.com/philhawksworth/status/1159193504851144705"}

[gulp.js](https://gulpjs.com/) is a great tool, I often forget how useful and versatile it can be. The homepage text sums up gulp.js pretty well: _"gulp is a toolkit for automating painful or time-consuming tasks in your development workflow, so you can stop messing around and build something"_. You use it in the command line in the form of [gulp tasks](https://gulpjs.com/docs/en/getting-started/creating-tasks).

For example, I could create a task called `styles` that turns a `.scss` file into a `.css` file, minifies that file and then copy it into my production directory. All by a running a single single command, `gulp styles`. Very handy if you want to make custom file processing workflows and already have some familiarity with Node / JavaScript.

## Coding

Right, so we have our base components to achieve a link between Ghost and a Jekyll site:
1. [Ghost](https://ghost.org): Where our content will be sourced from
1. [Ghost Content API Library](https://ghost.org/docs/api/v2/javascript/): How we're going to get the content
1. [gulp.js](https://gulpjs.com): How we're going to take that content and produce markdown files for Jekyll to consume

Because we're using gulp.js all the following code is inside a single `gulpfile.js`. If you're a bit unfamiliar with gulp I'd recommend checking out the [gulp.js documentation](https://gulpjs.com/docs/en/getting-started/quick-start) on how to get started and it's concepts.

### Source content via API

The [JavaScript Client Library](https://www.npmjs.com/package/@tryghost/content-api) for Ghost makes this a fairly clean process. I'm just using the demo API configuration so you'll need to replace this with the credentials of the Ghost site, more info on [how to get those credentials can be found here](https://ghost.org/docs/api/v2/javascript/content/#authentication). In a `gulpfile.js`:

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

}
```

### Construct an array of files

We've got our API data, but we loop through that data and produce files from each post item. Out of the box gulp is designed to take file A and turn it into file B. We'll need to bring in some dependencies that will allow us to turn that data into new files.

Here's what I ended up using:
- [streamArray](https://www.npmjs.com/package/stream-array): Taking the array of `posts` we've created and feeding that into Node
- [Vinyl](https://www.npmjs.com/package/vinyl): A library created by the gulp.js team for creating files within a gulp.js task
- [through2](https://www.npmjs.com/package/through2): I'm not entirely sure, but I think this is a wrapper that makes reading and writing of data in Node a bit cleaner

``` js
const streamArray = require('stream-array');
const File = require('vinyl');
const through = require('through2');

// ...

  // Begin iterating over posts
  return streamArray(posts)
    .pipe(through.obj(function (post, enc, callback) {

      // Getting some values from the post object
      const { published_at, slug, title } = post;

      // Take a single post and create a new file
      const file = new File({

        // Name the file based on the post date
        // and the slug
        path: `${published_at.slice(0,10)}-${slug}.md`,

        // Write the title of the post
        // inside the file
        contents: new Buffer.from(title),

        // Provide the post data inside the file
        data: post,
      });

      // All done, push file back
      // callback to start over again
      this.push(file);
      callback();
    }))

    // Put the files in a '_posts' directory
    .pipe(gulp.dest('./_posts'));
});
```

There's a fair bit happening in the above but I've done my best to explain it in the comments. Note that We're using the published date and slug of each post to construct the filename and placing them in a `/_posts` directory, which follows [Jekyll's post filename format](https://jekyllrb.com/docs/posts/#creating-posts). The `.slice(0,10)` is to remove the time from the full date string.

### Create frontmatter and markdown

The final part to this `gulpfile.js` task is taking the Ghost post data and formatting it in such a way that Jekyll will read it as a typical markdown post. Again, dependencies to the rescue!

Here we're using template strings to construct the format of our markdown files, and then handlebars ([gulp-hb](https://www.npmjs.com/package/gulp-hb) to be exact) to transform the variables into the values we want. We could just use regular javascript to put the data straight into the template, but this a bit easier to read and Could be extended upon without overly complex template strings.

``` js
{%- raw -%}
const hb = require('gulp-hb');

//...gulp.task

  // Create markdown template
  // using handlebars templating
  // (No indentation so it doesn't appear in the file)
  const markdownTemplate = `
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

  // ...streamArray

      // Write markdown template string into the file
      contents: new Buffer.from(markdownTemplate.trim()),

      // The contextual post data used
      data: post,
    });
    this.push(file);
    callback();
  }))

  // Pass files through handlebars templating
  // turning template code into actual values
  .pipe(hb())
  .pipe(gulp.dest('./_posts'));
});
{% endraw %}
```



## All together now!

<script src="https://gist.github.com/daviddarnes/eb956c1a8b57f4249ea57516b06ca89e.js"></script>

Pretty nifty method of bring Ghost and Jekyll together I think. Feel free to [chat with me on Twitter](https://twitter.com/DavidDarnes if you've got some improvements or are using this yourself!
