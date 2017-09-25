---
title: "Amber: Distributed Web Caching Service"
date: 2017-02-16 13:57:00 -0800
link: "http://amberlink.org"
draft: false
tags:
 - Internet
topics:
 - technology
---

[Amber][1] is an attempt from [Harvard's Berkman Klein Center for Internet & Society][2] to get content creators and publishing platforms to help distribute (or populate centralized) cached copies of linked content. By default it keeps locally (on your infrastructure) cached copies of content you've linked to in from your webpages so that if that content disappears you can still provide a working reference to that content. It will also allow you to use a centralized copy such as the [Internet Archive][3] for this same purpose. As of this posting they are providing plugins for Drupal and Wordpress as well modules for the Apache and Nginx HTTP web servers. 

Given the potential copyright issues (they do allow for content publishers to opt-out of the Amber content fetcher) I would prefer a centrally shared repository such as the Internet Archive to be the default storage mechanism but I do appreciate the single-point-of-failure flaw in that thinking. The pros & cons of local versus centralized storage would change based on the type of content you are publishing and referring to but my instincts say the "install and forget" crowd would be best served by leverage the amazing work done at the Internet Archives (via their "Wayback Machine".)

[1]: http://amberlink.org
[2]: http://cyber.law.harvard.edu/
[3]: https://archive.org
