# Python numpy shape-typing

One thing that I have fallen in love with, is Python typing.  Yes, I know Python is supposed to be an untyped language,
but that doesn't mean it doesn't have types.  In fact, it's very useful to know whether something is an integer, or a
list if you want to repeat another thing based on this.  Python typing is a non-strict way to describe the parameters
and return type of a function or script.  It's useful for humans because they understand what they should provide and
your IDE can give you suggestions based on what you may enter.

Numpy is a package for Python for **num**erical computations.  It provides efficient implementations for arrays and
matrix multiplications and many other things.  You can already see where this is going, because you obviously want to
also add type-hints to functions that work on matrices.  For instance the normal matrix multiplication requires the
inner dimensions of its operands to be equal ($\mathbf A\mathbf B=\mathbf C, \mathbf A\in\mathbb R^{N\times M},\mathbf
B\in\mathbb R^{M\times K},\mathbf C\in\mathbb R^{N\times K}$).  Unfortunately it's difficult to find a useful way to
add type hints that account for operations that add or remove a number of rows from an array.  In fact it may be
impossible for statically inferring everything, because that would probably lead to the ability to program with the
type hints, something that seems really weird.

The only reason I made this page is that I was looking into this today anyway for answering a question on a private
forum and I wanted a place to put the text below:

> There is a [PEP-646] accepted for Python 3.11 that goes into basic implementation for shapes, but it has not yet been
> implemented entirely for numpy and IDE type checking (mypy does not yet support `TypeVarTuple`).  The problem with
> implementing typing for what you're trying to do with `Array[D, 2*D]` is that it requires arithmetic and it's not
> obvious how arithmetic should interface with the other typing features.  You may wish to follow the
> [numpy GitHub thread][nptyping-gh] for this issue.
>
> For now, you can already type numpy arrays with [`np.typing.NDarray`][NDarray] that implies an array of any shape and
> any dtype and `NDarray[np.floating]` to imply an array of any shape, but floating point dtype.
>
> Actually, there are non-official implementations like [nptyping] and recently archived [data-science-types], but that
> thus requires extra packages that may not be available on Lisa and would require TA's to install them too.  I think
> [this SO question][SO-typing] provides a nice overview.

[PEP-646]: https://peps.python.org/pep-0646/
[nptyping-gh]: https://github.com/numpy/numpy/issues/16544
[NDarray]: https://numpy.org/doc/1.23/reference/typing.html#numpy.typing.NDArray
[nptyping]: https://pypi.org/project/nptyping/
[data-science-types]: https://github.com/wearepal/data-science-types
[SO-typing]: https://stackoverflow.com/questions/54503964/type-hint-for-numpy-ndarray-dtype
