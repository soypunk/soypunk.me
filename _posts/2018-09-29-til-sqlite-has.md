---
layout: post
microblog: true
audio: 
date: 2018-09-28 22:13:51 -0700
guid: http://soypunk.micro.blog/2018/09/29/til-sqlite-has.html
---
TIL: [SQLite has a readonly mode](https://www.sqlite.org/c3ref/open.html). Opening your database with this immutable data option means you avoid SQLite's concurrency issues enabling faster reads. I think SQLite is vastly underrated.
