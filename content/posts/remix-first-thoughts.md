+++
title = "Remix First Thoughts"
date = "2023-04-04T23:58:03-04:00"
author = "alexb"
cover = ""
tags = ["remix", "learning"]
keywords = ["", ""]
description = ""
showFullContent = false
readingTime = false
hideComments = false
+++

Following the [acquihire](https://remix.run/blog/remixing-shopify) late last year by Shopify and some strong praise for the Remix framework via Twitter, I clocked it as a high priority for my next learning endeavour. I started my software journey with Ruby and Rails so I have a penchant for the opinionated, and fittingly I felt like Remix deserved a bit of my attention. I spent a bit of time taking Remix for a spin, and decided to consolidate some of my thoughts.

## The Stacks
An interesting concept complete with très cool musical genre names, but I didn't really find the sweet spot. The curated stacks were a little too far along in the build cycle, and the generic template was a little too empty. I felt like I was either deleting a ton of unused logic, or adrift at sea hooking up the front and backend.

## The Remix Way
Combining the some of MVC logic into single files is interesting. I enjoyed a bit faster feedback when doing some model validations and transformations in views, but I found some of my files getting too long to read easily. This may just take some more time getting used to, but I still find it more intuitive logically dividing the MVC concerns into separate files, and homing in on them via a fuzzy finder.

## Nested Routes
According to the Remix documentation, a strong grasp of the routing logic is one of the most important things to understand in the framework. Sacrificing a bit of extensibility on your routes makes things much simpler to configure. I'm with the Remix team on this one. Most apps can (or should) be divided into nested routes and views. This really lends itself to dead simple PWA's and Mobile apps.

## Where are my Generators?
Rails gained a huge market share because it removed so much friction when creating an app. Remix is moving in the right direction artchitecturally, but missing some things in the DX world. A Rails-like generator script would really put the whole framework over-the-top by tightening feedback cycles. Again, in the same way that Remix has distilled the routing and views, some repeatable model logic could convince me to ditch old-school MVC's.

## Overall Thoughts
Even though I experienced some pain points, working with Remix is great. I plan on continuing to devote a significant amount of my learning time to it. Something that really resonated with me from the docs was the idea that Remix didn't over-use magic in their API. [Forms are Forms](https://remix.run/docs/en/main/components/form), and using Remix forms correctly makes you better at HTML forms. I'm still a big proponent of browser technologies ([Blog Post: Long Live the Browser](/posts/long-live-the-browser)), so I agree that web fundamentals will be valuable for the foreseeable future. 
