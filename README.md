# problem

Order regular expressions by the power of their languages.

## occurence

One time I was working on a rule engine for the web where metadata and other rules were to be applied to web pages based on some URL patterns.
Patterns and rules were changing too often to keep them encoded in the codebase.
Apparently pattern matching features were sufficiently covered by regexes, and related rules could be fetched based on what patterns matched what URLs.
The issue arises when there is more than one matching pattern.

# solutions

## solution A

The possibly simplest solution imaginable could be attaching a global manual ordering property to the pait of pattern-rules.
But that would in essence just put the burden of ordering patterns on a person.
Even with all included tools, like being quickly find what kinds of pages what patterns apply to, and what patterns were applied in what order to a page, it is burdensome.

## solution B

Fortunately, in my case, the required regular language was not that powerful, like PCRE, but closer to a much simpler glob.
Remapping the domain of "regular parts" (constant expressions, alterations, dicts and wildcards) onto a simple language (decimal numbers...) based on some obvious heuristics.
Provided strings then could be ordered lexicographically and resulting ordering satisfied all neccessary cases.
The solution is not total, but worked because all regexes were matching the same string, so a total ordering wasn't neccessary in the first place.
But the solution is also not entirely correct for all possible cases within this system, it only solves actually used cases, basically an opportunistic duct taping.
Having a solution that works for most cases and in unsurprising way was enough.

## solution C

I hope I'll ever come around to testing an approach where I try to count power of infinities for the regular expressions and order them by that.
Such solution will also probably not allow total ordering, but it will be able to more accurately solve the original task.
I also have a feeling that it won't be total for the subset of a more global problem as well (only ordering expressions that match the same string, and thus have intersecting language).
Some say that total ordering of regular languages cannot be defined.

## solution D

Something could probably be done by carefully analyzing the expressions and comparing their parts.
The complexity of the problem explodes if we try to also measure this for more complicated regular languages, like PCRE, that allow for lookaheads etc.

# observations

## sugar

Some regular expression features can be seen as sugar and therefore simplified to other equivalent expressions, e.g. unrolling wildcards: `..* === .+`.
Something of this sort should already be happening inside a regex engine.
For the purpose of only answering whether the expression matches the string, e.g. following kinds of equivalence could be made `^abc === ^abc.*`.
They would not be applicable to regular expressions in more general sense.


# materials

[Regular Expression Matching Can Be Simple And Fast](https://swtch.com/~rsc/regexp/regexp1.html)
[Derivatives of Regular Expressions](https://lcs.ios.ac.cn/~chm/papers/derivative-tr200910.pdf)
[Derivatives of Regular Expressions - Janusz A. Brzozowski (Modified)](https://github.com/katydid/regex-deriv-coq/blob/main/src/Brzozowski/Derivatives%20of%20Regular%20Expressions%20-%20Janusz%20A%20Brzozowski.md)
[Rewriting Extended Regular Expressions](https://tidsskrift.dk/daimipb/article/download/6934/5897)
[Testing the Equivalence of Regular Languages](https://arxiv.org/pdf/0907.5058)
[Regular-expression derivatives reexamined](https://www.khoury.northeastern.edu/home/turon/re-deriv.pdf)
[DFA minimization](https://en.wikipedia.org/wiki/DFA_minimization)
[Brzozowski derivative](https://en.wikipedia.org/wiki/Brzozowski_derivative)
[Testing the equivalence of regular expressions](https://www.dcc.fc.up.pt/Pubs/TR07/dcc-2007-07.pdf)
