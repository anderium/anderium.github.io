# Lambda (λ) Calculus

Is a mathematical functional programming language.  It is at the basis of automated proof checking, but also just fun to
play around with.  I recommend this tutorial by Evin Sellin: <https://lambdaexplorer.com/>.  The tutorial ends, as of
2024-07-11, with the following challenges:

1. Write the `Subtract 1` (`PRED`) function. (There are a number of tutorials you can find on this on the internet.)
2. Write the `Max(a, b)` function, a function that takes two numbers and outputs the larger of the two.
3. Write a function that computes the decimal equivalent of its input in [Gray code]. In other words, compute [A003188].

## My solutions

These challenges are a lot harder than the challenges before.  [Brilliant] says that Alonzo Church, the inventor of the
lambda calculus, couldn't solve the predecessor function for Church numerals himself.  Although one of his students,
Stephen Kleene, did manage to do so later.  Since we have the benefit of computers that allow us to try very quickly, I
thought it was worth a shot and came up with the following:

### `PRED`

```lambda
PRED := λx.λf.λn. x (λg.λa.a(gf)) (λa.n) (λi.i)
```

Initially, the idea was to use `TRUE` and `FALSE` to indicate whether the function `f` is the first of the number,
stripping itself if that was the case.  This was difficult to get right, because the parameters don't always ungroup how
I want them to.  The final eureka moment was to set `f` of the input Church numeral `x` be a function that generates a
function that adds the correct value (either the `f` or `n`).

Let's call the function that the number itself uses $f_0$ and the function that we provide the number $f_x$. (Used in
that order before.)  And let's define $n_0$ and $n_x$ similarly.

This implementation I wrote above drops the first instance of $f_0$ by filling in $n_x$ with a constant function that
ignores its parameter.  The function filled in for $f_x$ then applies this function on the preserved $f_0$, and creates
a new function that does not drop $f_0$.  I think it's easier to follow when you look at the reductions.

The first reduction takes `g = (λa.n)` and applies it on `f` to result in the function `λa.an`.  The second reduction
with `g = (λb.bn)` gives us `λa.a((λb.bn)f)` which reduces to `λa.a(fn))`.  You can find with induction that this is a
consistent process. However, this process will end with the final result being contained in that function for prepending
an $f_0$. Therefore, we extract it with the identity function.

Surprisingly, this is also the defenition for finding the predecessor that is on [Wikipedia].  (I did look there to see
if it was even possible without pairs, which Brilliant made it seem like it wasn't, but I only figured out that it was
the same function when I simplified my approach.)

### `MAX`

```lambda
SUB := λab.b PRED a
ISZERO := λx.x (λg.FALSE) TRUE
LEQ := λxy.ISZERO(SUB x y)
MAX := λab.(LEQ ab)ba
```

This is surprisingly easy once you've got the predecessor and subtract functions.  Only because that actually has a
quirk that `PRED ZERO` is still zero.  There's not much to say about this, honestly.

### Intermezzo `DIVMOD`

```lambda
DIVMOD := λab.a(λg.LEQ(PRED b)(gFALSE) (λf.f(SUCC(gTRUE))(ZERO)) (λf.f(gTRUE)(SUCC(gFALSE))) ) ((λxf.fxx)ZERO)
```

This function is actually pretty nice to think about.  It uses a pair to keep track of the current state, and updates it
with every function call to `g`.  It can be optimized to use the `ISZERO` function by counting down in the second
argument instead.  (757 instead of 610 reductions versus the original 793 on `DIVMOD 5 2`)  It doesn't, however, work
yet.  And apparently it isn't as good as I thought…

```lambda
DIVMOD2 := λab.(λpf.f(pTRUE)(SUBb(pFALSE))) (a(λg.ISZERO(gFALSE) (λf.f(SUCC(gTRUE))b) (λf.f(gTRUE)(PRED(gFALSE))) ) (λf.f(ZERO)b))
```

```lambda
ISEVEN := λa.a (λg.gFALSE TRUE) (TRUE)
DIVBY2 := λa.a (λg.gTRUE (λf.fFALSE (SUCC(gFALSE))) (λf.fTRUE(gFALSE))) (λf.fFALSE ZERO) FALSE
DIVMODBY2 := λa.(λfp.p(fFALSE)(fTRUE ONE ZERO))(a (λg.gTRUE (λp.pFALSE (SUCC(gFALSE))) (λp.pTRUE(gFALSE))) (λp.pFALSE ZERO))
MULTWITH2 := λxf.x(λg.f(f(g)))
```

<!-- Since FALSE and ZERO are equivalent (\f.fFALSE ZERO) can just be (\f.ZERO) -->

### `GRAY` code

Has a recursive definition `a(0) = 0; a(n) = 2 * a(floor(n/2)) + mod(floor((n + 1)/2), 2)`.  We can use this to generate
the decimal equivalent of the Gray code for `n`.  But first, me must figure out how to do recursion.

Recursion can be done with the construct `(λr.rr) (λfx.IFBASECASE BASEVAL (DOSOMETHING (ff RECURSE)))`.  I.e. to compute
the triangle number with recursion you can use this:

```lambda
(λr.rr) (λfx.ISZEROx x (ADD x (ff (PRED x)))) FOUR
(λfx.ISZEROx x (ADD x (ff (PRED x)))) (λfx.ISZEROx x (ADD x (ff (PRED x)))) FOUR
```

Factorial is almost identical, with the base case returning 1 instead and `ADD` being replaced by `MULT`.  Unfortunately
the site I recommend has a limit of 1000 reductions, which only allows these definitions to work up to input of 4.

Then, with the definition above for `DIVBY2` we can easily create the gray code's equivalent.

```lambda
QOOL1 := λabcd.a; QOOL2 := λabcd.b; QOOL3 := λabcd.c; QOOL4 := λabcd.d; QOOL0 := QOOL4
SELECTORMOD4 := λx.x (λg.gQOOL2 QOOL3 QOOL4 QOOL1) (QOOL4)
MODDIV42 := λa.SELECTORMOD4 a ZERO ONE ONE ZERO
GRAY := (λr.rr) (λgx.ISZEROx x (ADD (MULTWITH2 (gg (DIVBY2 x))) (MODDIV42 (SUCC x))))
```

This recursion transforms `((GRAY) INPUT)` into `((GRAY_without_r GRAY_without_r) INPUT)`, applying the function to
itself results in `(GRAY_applied INPUT)` where

```lambda
GRAY_applied := (λx.ISZERO ? 0 : 2 * (GRAY_without_r GRAY_without_r (INPUT / 2)) + LOWEST_BIT_CORRECTION)
```

#### Optimisations

Addition doesn't have to use the successor function, using the same idea you can write it a lot simpler.  In fact, you
can write an implementation that takes constant time, just like `SUCC` itself.  I.e. with complexity $O(6)$ versus
$O(4+3a)$, i.e. constant versus (linear in one of the inputs).

And for multiplication, this trick is almost identical.  It goes to complexity $O(3+2a)$ from $O(4+6a)$, no asymptotic
improvement, but it is useful for total reductions.  (And that analysis already uses the constant time `ADD` operation.)

`DIVBY2` goes to O(6+4a) from something quadratic O(n^2).

```lambda
ADD := λabfn.af(bfn)
MULT := λabf.a(bf)
DIVBY2 := λafn.a (λh.h(λtab.bt)(λtab.a(ft))) (λab.an) (λi.i) λi.i
```

This final improvement is the most important, obviously, and allows `GRAY` to work up to and including input of 13.

The created formula is not in normal form yet, doing this cannot be done at all, but if you ignore the recursion part
you can have it be created anyway!  A small tweak to the `MOD4DIV2` can also remove the `SUCC` from there.  This
squeezes out another few reductions, which is enough to also handle 14 with 980 reductions.

```lambda
(λr.rr)(λg.λx.(λx.x(λg.λa.λb.b)(λa.λb.a))xx((λa.λb.λf.λn.bf(afn))((λx.λf.x(λg.f(fg)))(gg((λa.λf.λn.a(λh.h(λt.λa.λb.bt)(λt.λa.λb.a(ft)))(λa.λb.an)(λi.i)(λi.i))x)))((λa.(λa.a(λg.g(λa.λb.λc.λd.b)(λa.λb.λc.λd.c)(λa.λb.λc.λd.d)(λa.λb.λc.λd.a))(λa.λb.λc.λd.d))a(λf.λn.n)(λf.λn.fn)(λf.λn.fn)(λf.λn.n))((λx.λf.λn.f(xfn))x))))

(λr.rr)(λg.λx.
  x(λg.λa.λb.b)(λa.λb.a)x  // if zero then zero
  // otherwise
  (λf.λn.
    // get correction
    (x(λg.g(λa.λb.λc.λd.b)(λa.λb.λc.λd.c)(λa.λb.λc.λd.d)(λa.λb.λc.λd.a))(λa.λb.λc.λd.a)(λf.λn.n)(λf.λn.fn)(λf.λn.fn)(λf.λn.n))
    f
    // added to 2 * (GRAY (INPUT / 2))
    (
      (gg(λf.λn.x(λh.h(λt.λa.λb.bt)(λt.λa.λb.a(ft)))(λa.λb.an)(λi.i)(λi.i)))(λg.f(fg))
      n
    )
  )
) INPUT

(λr.rr)(λg.λx.x(λg.λa.λb.b)(λa.λb.a)x(λf.λn.(x(λg.g(λa.λb.λc.λd.b)(λa.λb.λc.λd.c)(λa.λb.λc.λd.d)(λa.λb.λc.λd.a))(λa.λb.λc.λd.a)(λf.λn.n)(λf.λn.fn)(λf.λn.fn)(λf.λn.n))f((gg(λf.λn.x(λh.h(λt.λa.λb.bt)(λt.λa.λb.a(ft)))(λa.λb.an)(λi.i)(λi.i)))(λg.f(fg))n))) INPUT

r = recurse
g = gray
x = getal
f = getal functie
n = getal base
h = argument voor f in getal
abcd = [bq]oolean cases
i = identity
```

 <!-- reductions needed
 0:    8
 1:   48
 2:  128
...
 9:  690
10:  757
11:  794
12:  878
13:  915
14:  980

Seems around O(.5xx+60x) maybe?
-->

[Gray code]: https://en.wikipedia.org/wiki/Gray_code
[A003188]: https://oeis.org/A003188
[Brilliant]: https://brilliant.org/wiki/lambda-calculus/#church-numerals
[Wikipedia]: https://en.wikipedia.org/wiki/Lambda_calculus#Arithmetic_in_lambda_calculus


(\r.rr)(\g.\x.x(\g.\a.\b.b)(\a.\b.a)x(\f.\n.(x(\g.g(\a.\b.\c.\d.b)(\a.\b.\c.\d.c)(\a.\b.\c.\d.d)(\a.\b.\c.\d.a))(\a.\b.\c.\d.a)(\f.\n.n)(\f.\n.fn)(\f.\n.fn)(\f.\n.n))f((gg(\f.\n.x(\h.h(\t.\a.\b.bt)(\t.\a.\b.a(ft)))(\a.\b.an)(\i.i)(\i.i)))(\g.f(fg))n)))
