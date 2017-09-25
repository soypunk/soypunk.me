---
title: "State of Markdown Todo Item Syntaxes in 2014"
description: ""
draft: false
date: "2014-01-27T21:12:36-07:00"
tags:
- protocols and formats
topics: 
- technology
---
## Summary of Markdown Lists

As a plain-text person I generally gravitate to keeping my project materials in text files. As someone who believes HTML is the quintessential document format, I like to use Markdown to ease the transition from plain-text to sensibly structured HTML.

Naturally, one makes a lot of lists when taking meeting notes or capturing a list of tasks to be completed for a project. In Markdown single level lists are straightforward while multi-level lists, or outlines if you will, have all sorts of thorny edges depending on which Markdown parser you choose to use.

To begin a list item in Markdown one starts a line with `-`, `+`, or `*` followed by a whitespace character and then your list item text content.

Given Markdown's close relationship to HTML's text semantics it doesn't have a "task" or "todo" item syntax. Sure HTML Forms has `<input type="checkbox" />` but Markdown has never concerned itself with translating plain-text to HTML Forms markup.

Still Markdown is popular with the project documentation and note taking set and there are currently several attempts at employing a syntax for tasks. Here's a summary of them as well how backwards compatible these extensions are via the Babelmark test suite tool.

(At time of writing the Babelmark 1 testbed's Python Markdown implementation was failing due to a system error. I've removed those failures from the results.)

**Update 1/28/14, 10:47 AM PST:** I split out the Listacular/TaskAgent and TaskPaper/FoldingText sections as they really do have different behavior. Listacular (beta) is currently straddling two worlds though as it tries to support TaskPaper/FoldingText's `@done` syntax.

## GitHub Flavored Markdown Task list

[GitHub introduced this syntax extension on January 9th, 2013][ghfm-tasks]:

    - [ ] undone todo item  
    - [x] done todo item`

[ghfm-tasks]: https://github.com/blog/1375-task-lists-in-gfm-issues-pulls-comments

* [Babelmark Testbed Results (6 passes, 0 failures)][1]
* [Babelmark2 Testbed Results (17 passes, 3 failures)][1a]
    * These 3 failures are all related to not preserving whitespace within the undone todo bracket

[1]: http://michelf.ca/projects/php-markdown/dingus/babelmark/?markdown=-+%5B+%5D+undone+todo+item%0D%0A-+%5Bx%5D+done+todo+item
[1a]: http://johnmacfarlane.net/babelmark2/?text=-+%5B+%5D+undone+todo+item%0A-+%5Bx%5D+done+todo+item

## [Listacular][] / [TaskAgent][]

    - undone todo item  
    x done todo item

Neither of these are necessarily Markdown editors but both will accept subsets of the Markdown language for formatting. Listacular goes much farther than TaskAgent and is willing to render entire documents as Markdown and do its best to extract todo items (by looking at list items with the `-` marker rather than those with an `+` or `*`.)

* [Babelmark Testbed Results (0 passes, 6 failures)][2]
    * `x` is not a valid to signal to a Markdown parser that you wish to have a list item so naturally these fail.
* [Babelmark2 Testbed Results (20 failures)][2a]
    * Errors for the same reason as above.

[2]: http://michelf.ca/projects/php-markdown/dingus/babelmark/?markdown=-+undone+todo+item%0D%0Ax+done+todo+item
[2a]: http://johnmacfarlane.net/babelmark2/?text=-+undone+todo+item%0Ax+done+todo+item

## TaskPaper / [FoldingText][]
 
    - undone todo item  
    - todo item @done
 
To be fair, neither TaskPaper or FoldingText actually claim to be "Markdown" editors. They are more "Markdown based" or inspired. Still, people confuse them enough with the Markdown editor set that I think it is worth calling this out.

* [Babelmark Testbed Results (6 passes, 0 failures)][4]
* [Babelmark2 Testbed Results (20 passes, 0 failures)][4a]
    * Pandoc has an interesting side-effect of marking up the `@done` with `<span class="citation">@done</span>`

[4]: http://michelf.ca/projects/php-markdown/dingus/babelmark/?markdown=-+undone+todo+item++%0D%0A-+todo+item+%40done
[4a]: http://johnmacfarlane.net/babelmark2/?text=-+undone+todo+item++%0A-+todo+item+%40done
 
## [1Writer][]

    -- undone todo item  
    ++ done todo item

* [Babelmark Testbed Results (0 passes, 6 failures)][3]
    * None of the parsers were so generous as to accept initial the `-` or `+` symbol as a list item presumably because they are all looking for a whitespace character after one of these characters.
* [Babelmark2 Testbed Results (20 failures)][3a]
    * Similar to the above failures although Pandoc refused to even enter paragraph mode for the initial `--` item and kramdown actually barfed out a parser error.

[3]: http://michelf.ca/projects/php-markdown/dingus/babelmark/?markdown=--+undone+todo+item%0D%0A%2B%2B+done+todo+item
[3a]: http://johnmacfarlane.net/babelmark2/?text=--+undone+todo+item%0A%2B%2B+done+todo+item

## Results Conclusion

Only GitHub Flavored Markdown's Task list and TaskPaper/FoldingText's syntax survives mostly intact across most Markdown parsers. Sadly, almost none of the Markdown editors on the market use Github Flavored Markdown as their Markdown engine of choice. Mac OS X Markdown editor [Erato][] is an exception but without a sufficient matching mobile client in the iOS ecosystem there's little hope for a sane individual to hope to get by choosing this syntax. If omz:software's [Editorial for iPad][] ever makes it way to the iPhone a lot of us power users might be able to construct our own happy compromises. I can't really speak to the state of Markdown todo support on Android or Windows Mobile but I'm happy to reference others' research on this topic.

[1Writer]: http://1writerapp.com
[Editorial for iPad]: http://omz-software.com/editorial/
[Erato]: http://9muses.se/erato/
[FoldingText]: http://support.foldingtext.com/kb/frequently-asked-questions/how-does-foldingtext-relate-to-markdown
[Listacular]: http://www.bloomingsoft.com/listacular/
[TaskAgent]: http://taskagentapp.com
