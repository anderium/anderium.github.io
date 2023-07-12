# Taxi

The programming language [Taxi] allows you to write programs by driving passengers to different locations in a fictional
town.  Since you can write a [brainfuck] interpreter you can theoretically create all programs.

## Map

As I said, the program you write are instructions for a taxi in a virtual world.  Passengers are the data and locations
the operations, you always have to keep the [map] at the ready.  As you are driving, you have to take into account that
your fuel is used and so you need to stop by different stations.  You also can't just fuel unlimitedly, you first need
to earn money by dropping off pasesnger to be able to pay anything.

## Example program

```taxi
"anderium" is waiting at Writer's Depot.
Go to Writer's Depot: west 1st left, 2nd right, 1st left, 2nd left.
Pick up a passenger going to the Post Office.
Go to the Post Office: north 1st right, 2nd right, 1st left.
Go to the Taxi Garage: north 1st right, 1st left, 1st right.
```

## Golfing

Golfing refers to the process of writing code that minimises the number of characters in the solution.  It's a common
hobby for people programming in weird languages, and pretty fun to try.  For this language, there are a few quirks that
make golfed programs a lot shorter.  First of all, when specifying the directions, you do not need to write out `left`
or `right`: simply using `l` or `r` is specific enough.  When switching to a plan “if no one is waiting,” you can just
`Switch to plan A i.`  The conditional check is based only on the precense of text after the plan name.  Speaking of
plan names, you don't need any quotes if you don't use spaces.

I have published a few programs with explanations on the CodeGolf stackexchange that I'm proud of, so I'll quickly
summarise them here:

1. **Scream very loudly**: _Write a program that permanently outputs the character A._ [link][scream very loudly]
   I made two solutions that were equal length, but then I realised that I could just make it even shorter and I would
   lose the reason for my whole explanation.  Because it's still pretty interesting you can still find it there.
2. **Double Speak**: _Write a program that doubles every input character._ [link][double speak]
   Again, I found two solutions of equal length.  (If I had a nickle every time…)  This was a pretty fun challenge,
   even if it's very basic in its idea.

Surprisingly, you are actually restricted by the fuel for the payment you get for both these programs, contrary to what
I usually believe happens with complex programs.

[brainfuck]: ../brainfuck/readme.md
[double speak]: https://codegolf.stackexchange.com/a/229209/89860
[map]: https://bigzaphod.github.io/Taxi/map-big.png
[scream very loudly]: https://codegolf.stackexchange.com/a/195715/89860
[Taxi]: https://bigzaphod.github.io/Taxi/
