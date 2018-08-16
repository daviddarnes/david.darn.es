---
title: "Dropping the mic on Netlify in 20 minutes"
icon: tutorial
colour: "#00aea0"
excerpt: "Alright, so I didn’t actually drop the mic on Netlify; I dropped a site on it. Netlify Drop is a tool where you can grab a folder containing a site or app or whatever and drop it straight into the Netlify hosting platform."
---

![Mic drop on https://mic-drop.netlify.com](/images/mic-drop/mic-drop.gif)

Alright, so I didn’t actually drop the mic on Netlify; I dropped a site on it. [Netlify Drop](https://netlify.com/drop) is a tool where you can grab a folder containing a site or app or whatever and drop it straight into the Netlify hosting platform. You can [read more about Drop](https://www.netlify.com/blog/2018/08/14/announcing-netlify-drop---the-simplicity-of-bitballoon-with-the-added-power-of-netlify/) on the Netlify blog.

Anyway, I saw their announcement and thought...

> Hmm I really want to try this out, but what should I make?

And then it clicked... well, thudded - with a little audio feedback.

## Let’s begin
I started in a place where I often go to code obscure, but fun things: [CodePen](https://codepen.io/). Kicking things off with a bit of HTML:
<p data-height="144" data-theme-id="19615" data-slug-hash="RBmNMa" data-default-tab="html" data-user="daviddarnes" data-pen-title="Mic drop" class="codepen">See the Pen <a href="https://codepen.io/daviddarnes/pen/RBmNMa/">Mic drop</a> by David Darnes (<a href="https://codepen.io/daviddarnes">@daviddarnes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

So, I’ve got a mic and a hand to hold it neatly (if a little inaccessibly) wrapped in some `span` elements, but I need to sort out the presentation. There’s a set of styles that I almost always use when knocking together that needs to be front-and-centre, which is why I should probably throw these into a [CodePen template](https://blog.codepen.io/2018/05/24/a-new-create-menu-and-unlimited-pen-templates/), so I don’t have to write them every time:

``` css
body {
  min-height: 100vh;
  display: grid;
  place-items: center;
  font-size: 10vw;
}
```

What’s going on in the above CSS? Well, I’m selecting the body element and giving it a height of at least 100% of the browser height (viewport height, `vh`). Then, I’m harnessing the power of CSS Grid to centre any child elements within the body. I love the `place-items` shorthand property for centering grid items - totally stole that from [a tweet by Benjamin De Cock](https://twitter.com/bdc/status/877553112772423681). The last bit is a flippant attempt to scale the emojis with `font-size` in relation to the browser width (viewport width, `vw`).

These styles aren’t going to get the desired result, however. I need the hand to overlap the mic and rotate it a little to give the impression that it’s holding the mic:

``` css
span {
  grid-area: 1 / 1;
}

.hand {
  cursor: pointer;
  transform: rotate(-38deg) translateX(-20%) translateY(1%);
}
```

In this part of the CSS, I’m using `grid-area` to place the hand and the mic in the same grid cell; it’s an excellent trick to overlap elements without using absolute positioning. That’s another one I stole from someone, but this time it was in the [CSS Grid course by Wes Bos](https://cssgrid.io/). Lastly, shown above are a few adjustments to the hand with some `transform` styles, as well as making sure the cursor pointer comes up when someone hovers over the hand (bad Dave! Very inaccessible).

## Dropping the mic
Now, how to make this mic drop off the screen? For this, I’m going to employ the use of CSS custom properties:

``` css
.mic {
  transition: 1s ease-in;
  transform: translateY(var(--drop, 0)) rotate(var(--spin, 0deg));
}
```

With these styles, the `.mic` (the mic 🎤) will look no different and won’t do anything. However, it’s ready to take onboard two custom properties, `--drop` and `--spin`. These custom properties have also been setup with defaults to make sure they have a starting point: `var(--drop, 0)` for the Y translation (moving downwards) and `var(--spin, 0deg)` for rotation (in degrees). The other property is to tell the element to transition between states, so the mic will move whenever I give it any property change, custom or not.


## Listening for the cue
As the mic has been prepared for my two custom properties, I can now apply them when someone clicks on the hand with a bit of JavaScript:

``` js
document.querySelector('.hand').addEventListener('click', event => {
  event.target.innerHTML = `✋`
  document.querySelector('.mic').style = `--drop: 60vh; --spin: 900deg`
})
```

I’ve got a habit of writing short, but sometimes hard to read JavaScript, so maybe this will help you understand what I’m doing:

``` js
const hand = document.querySelector('.hand');
const mic = document.querySelector('.mic');

hand.addEventListener('click', () => {
  hand.innerHTML = `✋`
  mic.style = `--drop: 60vh; --spin: 900deg`
})
```

In the cleaner presentation above, I’m selecting both the hand and mic `span` elements and naming them, respectively. To the hand I’m adding an event listener, so I know when a `click` happens on it. Two things will then happen when the hand is clicked:

1. The content of the hand `span` will be changed to an open hand ✋
2. A `style` attribute will be added to the mic `span` with a value that contains new values for my custom CSS properties, `--drop: 60vh`  and `--spin: 900deg`

With this in place, the hand will ‘open’ and the mic will drop down 60vh (60% of the viewport browser height) and spin 900 degrees. I realise now that 900 degrees for a mic to spin after someone dropping it is a bit excessive, unless it was [Tony Hawk dropping it](https://www.youtube.com/watch?v=UnDgQUW1CO0).

## The result
<p data-height="300" data-theme-id="19615" data-slug-hash="RBmNMa" data-default-tab="result" data-user="daviddarnes" data-pen-title="Mic drop" class="codepen">See the Pen <a href="https://codepen.io/daviddarnes/pen/RBmNMa/">Mic drop</a> by David Darnes (<a href="https://codepen.io/daviddarnes">@daviddarnes</a>) on <a href="https://codepen.io">CodePen</a>.</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

The final slot of the puzzle was using what I mentioned at the start, [Netlify Drop](https://netlify.com/drop):

![Dropping a folder onto Netlify Drop](/images/mic-drop/drop.gif)

**You can find the final resulting hosted site at [https://mic-drop.netlify.com](https://mic-drop.netlify.com)**

## Conclusion
This was really fun to make, and thanks to all these great tools and development features, it only took 20 minutes or so to complete. There have been [so many people responding to it on Twitter](https://twitter.com/Netlify/status/1029662360192069632) and it’s [great to see](https://twitter.com/dataandme/status/1029802654720045056) [people enjoying it](
https://twitter.com/philhawksworth/status/1029669405146472448) and [having a laugh](https://twitter.com/DavidWells/status/1029891166219591680).

## To do
This subheading sounds ominous, as if I’m going to make it into some kind of SaaS product or something. Well, I can tell you now, that’s not ****my plan - I want to use it for learning purposes. There are some things I want to try out which include a couple of the other useful features Netlify provides. Here’s what I’m thinking:

- **Stop the mic spinning so much**: the mic is dropping, not dancing
- Make sure the **mic is in front of the open hand**
- **Fix the bug on iOS Safari**: browser height is changing and `vh` tries to keep up. Sadly, Safari iOS is pretty bad at this and there [has been quite a bit of work to work around the bug](https://medium.com/samsung-internet-dev/toolbars-keyboards-and-the-viewports-10abcc6c3769#e8fd)
- **Use a Lambda function to log every mic drop** that happens on the site and show it as a rolling tally. [Netlify has this as one of it’s backend features](https://www.netlify.com/features/#add-ons)
- Allow repeatable ‘drops’ to give people the extra satisfaction
- A query string of some kind on the url, so that the mic automatically drops whenever someone opens the link - to give *other people* the satisfaction

Alright, I think that’s everything. I’ve gone on for too long now. Thanks for reading! If you liked this, then [feel free to share it](https://twitter.com/home?status=Dropping%20the%20mic%20on%20%40Netlify%20in%2020%20minutes%20https%3A//david.darn.es/2018/08/16/dropping-the-mic-on-netlify/%20by%20%40DavidDarnes) or [send me a nice tweet](https://twitter.com/DavidDarnes).
