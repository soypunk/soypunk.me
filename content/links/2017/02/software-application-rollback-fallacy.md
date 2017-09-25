---
title: "Software Application Rollback Fallacy"
link: https://blog.skyliner.io/you-cant-have-a-rollback-button-83e914f420d9#.58p134oe9
date: 2017-02-28 10:54:00 -0800
draft: false
topics:
 - technology
---

Dan McKinley, formally of Stripe and Etsy and now at [Skyliner][], writes:

> I've worked with deploy systems in the past that have a prominent “rollback” button, o
> a console incantation with the same effect. The presence of one of these is reassuring,
> in that you can imagine that if something goes wrong you can quickly get back to safety
> by undoing your last change.
> 
> But the rollback button is a lie. You can’t have a rollback button that’s safe when 
> you’re deploying a running system

I was always the odd man out at several organizations where that believed they could safely rollback software updates as long as they had enough scripts, backups, and time. I personally felt this was at odds with the facts that data your users create keeps moving forward regardless of the bugs or issues you may have introduced. It also always seem to vastly underestimate the amount of effort needed to rollback software systems.

"Roll forward" is a term made popular by Flickr's engineering team and I've always thought it best described how to responsibly react to software problems with production systems. Dan's post gives some tangible examples of the "little things" that are hard to work around in the rollback scenario. It is also a good case for Dan's other mantra: [Choose Boring Technology][2] -- so you can fully understand the implications of your software system design decisions.

[Skyliner]: https://www.skyliner.io
[2]: http://mcfunley.com/choose-boring-technology?ref=related
