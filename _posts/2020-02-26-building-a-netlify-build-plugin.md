---
title: "Building a Netlify Build Plugin"
excerpt: "Netlify [Build Plugins](https://www.netlify.com/build/plugins-beta/) allow you to tap into the different phases in the build process that happen on Netlify. After being invited to the beta I spent some time figuring out what I could do and build a plugin of my own."
icon: article
category: article
colour: "#00506b"
image: "/images/netlify-build-plugin/netlify-build-plugin-banner.png"
published: false
---

![Main banner graphic]()

Netlify [Build Plugins](https://www.netlify.com/build/plugins-beta/) allow you to tap into the different phases in the build process that happen on Netlify. After being invited to the beta I spent some time figuring out what I could do and build a plugin of my own, a [build plugin to generate markdown from Ghost](https://github.com/daviddarnes/netlify-plugin-ghost-markdown).

## What are Netlify Build Plugins?

Every time Netlify starts a build it begins a 'cycle'. A cycle is made up of a [series of events](https://github.com/netlify/build#build-lifecycle):

1. `onInit`
1. `onPreBuild`
1. `onBuild`
1. `onPostBuild`
1. `onSuccess`
1. `onError`
1. `onEnd`

All these events happen in the above order, exceptions being `onSuccess` and `onError` for successful and failing builds respectively. Build Plugins give you the chance to step in with your own code at any of these lifecycle events. You can use vanilla JavaScript in a directory within your project, or some wrapped up in an npm package. You can read more about them on the [official GitHub repo](https://github.com/netlify/build#readme) as well as [this article by Sarah Drasner](https://www.netlify.com/blog/2019/10/16/creating-and-using-your-first-netlify-build-plugin/).

## What can you use them for?

Well, to be frank with you, I wasn't entirely sure. For quite a while after the announcement I thought "If I want to run some code before my build I'll add it in before my build in the project 🤷🏼‍♂️". However after looking at some of the examples my mindset began to shift, e.g. a [plugin by Peter Müller which checks links](https://github.com/Munter/netlify-plugin-checklinks) at the `onPostBuild` event and stops the deployment if there's a broken link in the build.

![Example build plugins]()

It wasn't until a late drive home from [NA Conf](https://newadventuresconf.com/2020/) while listening to [Fish and Scripts](https://fishandscripts.com/) that an idea dawned on me. I had already encountered a use case before, but with the use of plugins I could improve it. Not too long ago I wrote a tutorial on [how to use Ghost with Jekyll](https://david.darn.es/tutorial/2019/08/11/use-ghost-with-jekyll/), where I used [gulp.js](https://gulpjs.com/) to pull in content via the [Ghost Content API](https://ghost.org/docs/api/v3/javascript/content/) and generated markdown files for [Jekyll to comfortably consume](https://jekyllrb.com/docs/posts/).

It was a clever solution, but not what I would call 'clean'. Using gulp.js locally would mean you'd have to commit untouchable markdown files to your repo, because they're sourced from your install of Ghost. Using it on Netlify was much better but you're still using a pair of mismatched build tools, gulp.js and Jekyll.

![Compared steps between gulp method and build plugin method]()

If I was to tap into the `onPreBuild` phase of the Netlify build lifecycle I could generate the markdown files at that point and then let Jekyll run its normal course. I could also wrap the code up in a neat plugin that others could use, possibly with other static site generators to Jekyll!

## The set up

Netlify Build Plugins can be written in Node JavaScript wrapped in a module, aka `module.exports`. Plugins can tap into any event in the lifecycle, even multiple events. Here's how my plugin uses the `onPreBuild` event:

```js
module.exports = {
  name: "netlify-plugin-ghost-markdown",
  onPreBuild: async () => {
    // Using async so Netlify waits for it
  }
};
```

To make Netlify aware of this file it needs to be referenced in the configuration file. When working on this plugin I really struggled to get my head around the `.toml` format. Thankfully `.yaml` files are are supported within the beta as well.

Build plugins can be local, by referencing a directory, or an installed dependency.

``` yaml
plugins:
  - package: "netlify-plugin-ghost-markdown"
```

Check out the [Build Plugins repo readme](https://github.com/netlify/build#netlify-configuration) for more details.

## Using dependencies

It gets a bit meta when using dependencies in a local plugin because you'll essentially be starting up a new mini JavaScript project, `package.json` and all. That's partly why I wrapped the plugin in an npm package. That being said, if you're familiar with JavaScript and importing dependencies you're going to be comfortable with this.

```js
// Example dependency includes
const path = require("path");
const fetch = require("node-fetch");
const ghostContentAPI = require("@tryghost/content-api");
```

## Config variables

For my plugin to work for everyone I needed a way to let them configure it from the `netlify.yaml` file in their project. Build Plugins use the following syntax to state variables:

```yaml
plugins:
  - package: "netlify-plugin-ghost-markdown"
    config:
      ghostKey: "1234567890"
      assetsDir: "./images/"
      pagesDir: "./pages/"
```

The plugin can then pick up these variables like so:

```js
module.exports = {
  name: "netlify-plugin-ghost-markdown",
  onPreBuild: async ({
    pluginConfig: {
      ghostKey,
      assetsDir = "./assets/images/",
      pagesDir = "./"
    }
  }) => {

    // Logging them here as an example of context use
    console.log(
      ghostKey,
      assetsDir,
      pagesDir
    );

  }
};
```

Default function parameters are pretty handy here too. I was able to set the default pages and posts paths to what Jekyll would expect, but can be overwritten for SSGs like [Hugo](https://gohugo.io/getting-started/directory-structure/) or [Eleventy](https://www.11ty.dev/docs/data-template-dir/).

## Using a plugin

At first I thought when using a Netlify Plugin you only needed to reference it in the `netlify.yaml` file, however you do also need to install it as an npm package like so:

```bash
npm install --save netlify-plugin-ghost-markdown
```

So if you're using my plugin in a Jekyll project it's going to look a bit strange having a `package.json` in there too. Sign of the times I guess.

Then it's a matter of referencing and configuring the plugin in the `netlify.yaml`:

```yaml
plugins:
  - package: "netlify-plugin-ghost-markdown"
    config:
      ghostURL: "https://YOURGHOST.URL"
      ghostKey: "YOURGHOSTKEY"
```

## Wrapping up

I've provided [installation and usage instructions](https://github.com/daviddarnes/netlify-plugin-ghost-markdown#netlify-ghost-markdown-build-plugin) in the repo for my plugin. You're also welcome do dig around the code. It's less complex than other plugins I've seen, which may help you to get your head around the concept.

If you're using this plugin let me know! Feel free to share this article and let me know if it helped you too.

✌️
