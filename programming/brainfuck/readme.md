# Brainfuck

The programming language brainfuck, or brainf*ck, contains only 8 instructions, yet you can do everything, theoretically
(it is Turing complete).  I've programmed in it and can attest that it is fun, you should try it!  The website
[copy.sh/brainfuck][copyshbf] has a nice interface to start learning and create more complex programs.

## Example program

```brainfuck
++++[->+++++[->+++++>+++++<<]>+++<<]>>>---.<--.>+++.+.<++++.>++++.<+++.--------.
```

## Visual Studio Code

You can also download some code-highlighting extensions for most popular IDE's, which can be useful if you downloaded a
program.  There's also an interpreter for VS Code, but I didn't like it after trying shortly.  I'm hoping to one day
actually create a more full-fledge one, but so far I did not spend enough time to learn how to create an extension I'd
personally want to use.  If I do work on that, I'll post about it here, I guess?  The idea is to have a code
highlighter, interpreter and debugger that are meant to work together.

## Golfing

Golfing refers to the process of writing code that minimises the number of characters in the solution.  It's a common
hobby for people programming in weird languages, and pretty fun to try.  I don't remember whether I have any cool
examples that I made myself, so I guess not.  If I do find or create something I'll definitely put it here.  There's
also some tricks to improve your golfing, would you want me to create a page with that?

## Encoding and compressing

By default, brainfuck programs are written with ASCII (or UTF-8) and only the operations that have a meaning are
interpreted.  Of course, you can easily compress any brainfuck program by simply removing all non-operator characters,
but you can easily improve upon this.  There are only 8 operations and because $2^3=8$, we can further compress all
programs by 62.5%.  This might be slightly inefficient to decode, as the operations aren't byte aligned, but a 50%
compression by using 4 bits would be fine if that speed is necessary.

As soon as I intended writing this section, I realised that the obvious compression of 3 bits per operator might be
unbalanced, some operators occur much more or much less frequently than others.  I came up with two different
compressions that might reduce file size even more, which you can see in the Table below.  Before you look at it,
though, I would like to point out that compressing this way does not have to be optimal.  There are many other
compression algorithms that have been proven to work well on text and these algorithms will very likely also perform
well for compressing brainfuck programs.

Op | bits
---|---
\+ |  10
\- |  11
\> | 010
 < | 011
 [ | 001
 ] | 0001
 . | 00001
 , | 00000
   |
 [ | 0011
 ] | 0010
 . | 0001
 , | 0000

## Variants

As always with things that become popular, there will be variants that pop up.  I don't actually know how any variants
work, but one I like the concept of is [`jsfuck`].  While not being an extension to brainfuck, it is possible to write
Javascript programs using only six characters (`()[]+!`).  This can actually have security implications when allowing
user code on websites, because it means simply scanning for attempted XSS-attacks isn't enough.  eBay allows sellers to
provide their own script and according to [ArsTechnica][ebay-sec] they do not want to fix this issue.  (So whenever you
shop at eBay, remember you could be at risk.)

[copyshbf]: https://copy.sh/brainfuck
[ebay-sec]: https://arstechnica.com/information-technology/2016/02/ebay-has-no-plans-to-fix-severe-bug-that-allows-malware-distribution/
[`jsfuck`]: https://en.wikipedia.org/wiki/JSFuck
