I recently [joined Jason Lengstorf](https://youtu.be/pOGjVNC1sk4) on his Twitch show [Learn With Jason](https://www.learnwithjason.dev/). During the livestream we demonstrated the possibilities of using Ghost as a Headless CMS, using the [Ghost Content API](https://ghost.org/docs/api/v3/javascript/content/) with [Gatsby](https://ghost.org/docs/api/v3/gatsby/), [GraphQL](https://ghost.org/docs/api/v3/gatsby/graphql-recipes-for-ghost/) and [Eleventy](https://ghost.org/docs/api/v3/eleventy/).

I had a great time chatting with Jason and the audience. However in all the excitement I didn't get around to answering all the questions popping up in the live chat. Thankfully with the power of Twitch Chat Reply and an [npm script called 'twitch-chatlog'](https://github.com/freaktechnik/twitch-chatlog) I was able to go back in time and pull out all the questions people had during the livestream.

Here's a somewhat brief Q & A on those questions:

> [streamingRafa](https://twitch.tv/streamingRafa/): How can I become a Ghost?

The more I think about this question the darker it becomes. I'm not willing to answer.

> [redetg](https://twitch.tv/redetg/): so Ghost is like WordPress of node?

Ghost is CMS focused on publishing, built on Node.js. I'd highly recommend checking out our [WordPress comparison page](https://ghost.org/vs/wordpress/), it'll show you what the differences are and help you decide if Ghost is right for you.

> [me8bot](https://twitch.tv/me8bot/): Is he ghosting us?

Definitely not heard this one before… but seriously, sorry if I missed your question the first time round.

> [thedotmack](https://twitch.tv/thedotmack/): What do we do about custom fields, and is there a way to make custom cards?

I attempted to answer this question during the livestream, but I can't really reply without asking 'what are you trying to achieve?'. You'll be surprised what you can do with Ghost. Key value pairs tend to be an easy answer for developers to grab, rather than thinking further into what the final goal is.

> [streamingRafa](https://twitch.tv/streamingRafa/): Can you use Ghost to make a sandwich?

I mean, I guess? Ghost would be a good way to write up sandwich recipes? 

> [vinny_code](https://twitch.tv/vinny_code/): [Is Ghost a sandwich?](https://isthisasandwich.netlify.com/)

No, it is not…

> [thorsmightyarse](https://twitch.tv/thorsmightyarse/): Ghost is a CMS right?

Yes, it is!

> [thorsmightyarse](https://twitch.tv/thorsmightyarse/): Aren't we gonna do a from scratch without the starter?

Yes! You totally can, and we did. Check out [the repo Jason put up](https://github.com/jlengstorf/lets-learn-ghost) which contains an Eleventy site we put together from scratch during the livestream.

> [thorsmightyarse](https://twitch.tv/thorsmightyarse/): So I could use this with Eleventy?

Heck yea! I mentioned on the livestream I'm trying to rebuild my site with Ghost and Eleventy at the minute. I'm using [our Eleventy starter](https://github.com/TryGhost/eleventy-starter-ghost) as a base.

> [thorsmightyarse](https://twitch.tv/thorsmightyarse/): So Ghost is mainly focussed on making it easy to create a blog?

Pretty much. Ghost is all [about publishing](https://ghost.org/features/), blogging is a great example of that.

> [thedotmack](https://twitch.tv/thedotmack/): So I wanted to use a video on a page. I put it in a card. Embed card, and then moved it with javascript. Instead of bringing data in to the handlebars template

Sounds like you nailed the use of embed cards, nice job! [Cards in Ghost](https://ghost.org/faq/using-the-editor/#using-the-dynamic-menu) allow you to drop code blocks, YouTube videos, CodePen demos and all sorts of things directly into your content. The custom embed and HTML cards are probably the most appealing to the developers amongst us, allowing you to drop completely custom HTML right in the middle of your posts and pages.

> [thepaulmcbride](https://twitch.tv/thepaulmcbride/): We're using Ghost in work to power a Gatsby site. It is 😍

Awesome! If you read this post please share it, would love to see how Ghost is being used in the wild 👀

> [SchabrechtsK](https://twitch.tv/SchabrechtsK/): Spooky? Spoopy?

Pretty spooky, really spoopy 👻

> [programatiko](https://twitch.tv/programatiko/): Could you show Gatsby/GraphQL pulling stuff from Ghost? 🙏

I think we did cover this in the stream, however if you want some more examples of using GraphQL with Ghost then check out [this recipes page in our docs](https://ghost.org/docs/api/v3/gatsby/graphql-recipes-for-ghost/).

> [SchabrechtsK](https://twitch.tv/SchabrechtsK/): I tried WP but it's so slow :(
> [andrewlitchford](https://twitch.tv/andrewlitchford/): Story of my life

😶

> [thorsmightyarse](https://twitch.tv/thorsmightyarse/): What would be the differences/advantages of using Ghost compared to Netlify CMS with Eleventy?

I'd say the key differences are the editing experience and the way data is stored. Ghost provides a strong publishing experience out of the box, while Netlify CMS can provide a really custom editing experience if you're willing to put the work in. Ghost stores it's data in a database, while Netlify CMS stores data in the repo files.

I think their advantages over each other would only come through when set against the task at hand. Essentially, you need to work out what tool is best for the job.

> [philhawksworth](https://twitch.tv/philhawksworth/): Can you expose content from Ghost which is draft, staged and publish? Different API endpoints?

For sure! Only published posts are exposed in the Content API, however the Admin API gives you access to drafted and scheduled posts as well. You can find out more in [our API docs](https://ghost.org/docs/api/v3/javascript/admin/).

> [SchabrechtsK](https://twitch.tv/SchabrechtsK/): Does Ghost also do that _(provide an API)_ out of the box? So without Gatsby?
> [thorsmightyarse](https://twitch.tv/thorsmightyarse/): Don't understand why you would need GraphQL for building static site though?

Ghost has a great [API](https://ghost.org/docs/api/v3/) for pulling content, and the [JavaScript Content API Client Library](https://ghost.org/docs/api/v3/javascript/content/) makes your content even more accessible. It's one of the main reasons I was so keen to make the Eleventy starter, because the API fit really well with Eleventy's main configuration file.

You don't have to use GraphQL, you can use the JavaScript Content API that I mentioned before. However if you want to plug Ghost into an existing React or Gatsby site then the [gatsby-source-ghost source plugin](https://github.com/TryGhost/gatsby-source-ghost) might be the way to go.

> [andrewpgilliland](https://twitch.tv/andrewpgilliland/): So content creators would need Ghost downloaded on their device?
> [philhawksworth](https://twitch.tv/philhawksworth/): ...is there a hosted Ghost service or do authors have to have a self-hosted instance?

I think you're getting confused with the local install of Ghost we used. Ghost is completely [open source](https://github.com/TryGhost/Ghost), you can go ahead and install it locally without barriers. Doing so will create a local install of the Ghost admin interface and a site running alongside it. However for other people to see your site, and for your deployed [JAMstack](https://jamstack.org/) site to retrieve content from it, you'll need to have a hosted installation running somewhere on the internet.

For hosting options you could use something like [DigitalOcean](https://www.digitalocean.com/), they even have [a 'Droplet'](https://marketplace.digitalocean.com/apps/ghost) for you to spin up a Ghost installation quickly. While this is probably the cheapest option you do still have to maintain the installation yourself, if you're like me you won't enjoy server maintenance.

The alternative is [signing up for Ghost(Pro)](https://ghost.org/), which is our platform offering. We handle all the hosting and maintenance for you, and provide customer support whenever you need it. Check out [our pricing page](https://ghost.org/pricing/) for a full breakdown on features and benefits. Jason covered the topic of [time over money really well during the livestream](https://youtu.be/pOGjVNC1sk4?t=2885).

> [saiyugi](https://twitch.tv/saiyugi/): For the preview section of Ghost admin, can we point it to the custom front-end say the GatsbyJS website to show up in the preview of Ghost admin panel?

Yes! I made this handy snippet that will redirect all your pages to your JAMstack counterpart which you can drop into your site footer code injection area within your Ghost admin:

<script src="https://gist.github.com/daviddarnes/983142e7a2fce94044df0c87ffa7d39c.js"></script>

This snippet also accounts for previews which will be best shown in the internal Ghost theme layer.

> [NMeuleman](https://twitch.tv/NMeuleman/): Requesting permission to tweet: ["mood while coding"](https://clips.twitch.tv/LongAssiduousZebraRlyTho)

<iframe src="https://clips.twitch.tv/embed?clip=LongAssiduousZebraRlyTho" frameborder="0" allowfullscreen="true" height="378" width="620"></iframe>

Extremely relatable, very tweetable.

> [saiafonua](https://twitch.tv/saiafonua/): Zach Leatherman would be proud of you two

I sure hope so 💚

> [benidibatia](https://twitch.tv/benidibatia/): Do you guys have a website where I can go through steps by steps to get started with Ghost?

Best places to check out are our [documentation](https://ghost.org/docs/), [tutorials](https://ghost.org/tutorials/) and [community forum](https://forum.ghost.org/) filled with helpful references on using Ghost.

> [saiafonua](https://twitch.tv/saiafonua/): Thank you Jason and Dave! Awesome episode!

Thank **you** for joining the livestream! Hopefully we'll get to do this again sometime.

!["Tweet of Rafa toasting to our stream with wine"]

✌️
