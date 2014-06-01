---
title: Argumented Testing
----

I've finally gotten round to ensuring [diceroll](https://github.com/borntyping/diceroll) has a set of unit tests, and along the way I've ended up creating a very small, but useful testing library, called `argumented` (as it lets you agument tests with arguments!).

The library provides a few functions for 'packing' argument sets to be passed into a function or unit test, and a decorator for unpacking a class using these functions and replacing said functions with a set of functions that each call one of the given argument sets.

You can read more about it [here](https://github.com/borntyping/argumented).
