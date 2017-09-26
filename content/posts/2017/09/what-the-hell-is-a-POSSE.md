---
title: "What the hell is a POSSE?"
date: 2017-09-25T22:53:00-07:00
draft: false
tags:
 - IndieWeb
topics:
 - updates
---
This is a more technical follow-up to an [earlier post today][1], if you aren't really into that you can just tl;dr this.

Manton Reece really stirred things up for me when he said:

> Motivation for folks who have only blogged a few times this year: I've posted 468 times. The key is a "blog first, tweet second" strategy.
> http://www.manton.org/2017/09/5726.html

Twitter (at least for me) has a very sticky quality to it, in that I use it for reading news, research, answering questions, and a public scratchpad of notes. The problem often is, I want to say much much more than a single Tweet can contain but the immediacy (and distractions) of Twitter make it fairly easy to never get around to that.

Manton's "blog first" mantra really hit a chord and I was instantly reminded of IndieWeb's <abbr>POSSE</abbr> principal or [Publish (on your) Own Site, Syndicate Elsewhere][3] and wondered how I might go about that. Now if you have a ["fried"][4] content management system (e.g. Wordpress) this isn't terribly hard and you can own your content fairly quickly and start syndicating with a few plugins. I happen to "bake" my content with [Hugo][5] mostly because it is just less painful for me to administer, backup, and tinker with a statically generated website. (Hugo has also been a good way to understand some basic things about how the Go Programming language works.)

Baking the content means that there's no dynamic system always running to say "new entry of type X so also publish it to social site Y." But I do happen to have some triggers for new content. All of the sites' content is stored in a git repo. The git repo fires off a webhook when a new commit comes in this triggers the Hugo rebuild and that rebuilds the RSS Feeds. I can then attach additional scripts (in this case, written in Python 3) to parse the RSS feeds and republish the necessary material to Twitter (or wherever else.)

For Python at least this is rather straightforward. Use FeedParser for your RSS parsing and then pick from one of several well-maintained Twitter API clients. The secret sauce though for getting some nuances of Twitter right is this wonderful library: [twitter-text-python][6]

A Tweet has become surprisingly complicated. Most of us know that a Tweet must contain no more than 140 characters but there's a bunch of nuance to this. In my case we start with 140 unicode characters but that is easily handled with Python 3. We also have to decode the embedded HTML content inside the RSS items back to Unicode, again no big deal. The tricky part is counting characters for things Twitter gives you a pass on: @names and URLs in particular. But the twitter-text-python library parses all of these bits out for you so you can remove (or in the case of URLs, reduce) their hit on the character limit.

There's some initial code right now for handling these issues and hopefully I've gotten it right. Post and Link entries should tweet out their Titles with a link back to this site. Minis should tweet out their full content and only link back here if I've gone over the character limit. I still need to add in support for a Mini post with an image but it looks easy enough.

Of course this doesn't deal with edits and deletes yet but then those things were always a pain-in-the-ass on Twitter anyway so I'm not sure I've lost anything. Happy hacking friends!


[1]: https://soypunk.me/posts/2017/09/25/why-blog-again/
[2]: http://www.manton.org/2017/09/5726.html
[3]: https://indieweb.org/posse
[4]: http://www.aaronsw.com/weblog/000404
[5]: https://gohugo.io
[6]: https://github.com/edburnett/twitter-text-python