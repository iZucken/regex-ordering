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

- [Regular Expression Matching Can Be Simple And Fast](https://swtch.com/~rsc/regexp/regexp1.html)
- [Derivatives of Regular Expressions](https://lcs.ios.ac.cn/~chm/papers/derivative-tr200910.pdf)
- [Derivatives of Regular Expressions - Janusz A. Brzozowski (Modified)](https://github.com/katydid/regex-deriv-coq/blob/main/src/Brzozowski/Derivatives%20of%20Regular%20Expressions%20-%20Janusz%20A%20Brzozowski.md)
- [Rewriting Extended Regular Expressions](https://tidsskrift.dk/daimipb/article/download/6934/5897)
- [Testing the Equivalence of Regular Languages](https://arxiv.org/pdf/0907.5058)
- [Regular-expression derivatives reexamined](https://www.khoury.northeastern.edu/home/turon/re-deriv.pdf)
- [DFA minimization](https://en.wikipedia.org/wiki/DFA_minimization)
- [Brzozowski derivative](https://en.wikipedia.org/wiki/Brzozowski_derivative)
- [Testing the equivalence of regular expressions](https://www.dcc.fc.up.pt/Pubs/TR07/dcc-2007-07.pdf)
- [Equality, containment and intersection among regular expressions via symbolic manipulation](https://hackage.haskell.org/package/regexpr-symbolic](https://sulzmann.blogspot.com/2008/12/equality-containment-and-intersection.html)
- [Partial derivatives of regular expressions and finite automaton constructions by Valentin Antimirov](https://pdf.sciencedirectassets.com/271538/1-s2.0-S0304397500X00084/1-s2.0-0304397595001824/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjEEUaCXVzLWVhc3QtMSJIMEYCIQDEJpZjroDezSmvQOkqG5g7Kr%2BKDBipQRHf2ueXwL1DTAIhANB8Nj%2BzmVki9hrxTwzbQCEbx8RsiuFr2J1VwEpiHq0QKrMFCH4QBRoMMDU5MDAzNTQ2ODY1IgwF5C4x30Yzg4UocywqkAUIvcTc1lRQpMY%2F5%2Beccr6ND5nHEOCJPXwa39ATwJtHTOBymOqYSTZLOgS7lrArtMVakBJymzKpSoz%2BHRcGh1xrtJ0NXzWfBryaYcuQbSvG%2FRvJi6GVMkeXt4N3xE3fZWIkTK3sCHzvtetgEN2xZatroHURtuBKDE%2BuuDgIEfbMg5FkCH54zK8xwDn3meqEvuaLUeSnMK%2BgvVpfBwdtj9k24B14Pe1BYXMAHXlhfzUALqtSK7vYKpzPr4I%2Bs6OEsPXhYDtgYTZ2qRJaiBbXvTODE47WLT1xG3oaYcz6TppNQ4%2F1umUzgpdDqec%2BD0wHTu5ia4w26R938vrliEuh7ITkFpMJ9XCVtuCPbqIWqANTKS%2Bd3ziSkOVFyQg5Ff%2BhvJ3SPaRin%2FITyDLzbVQZN%2Bf5UEOFcvZeMPvef4GTGwOgiAGpiIJIB%2BSJv6L2ztc7ofJ81R9%2FLpSXPil1j%2BM%2FSqW%2B33NA7aa8SUREYikXlFmqCzFQeUpfkjwR3XhYNQ9FCy6soW%2B7y5IFac9e1BQSniXld0ujDAsZ3R7RYxrZgNcoDmofLix%2B2PMgb6x39ljmFH5TVfHSDK9O5M3Z4P7%2FU8rkUboprjL8mbLIJJGudCbYkk1f%2FKMPUA%2F1LaHftKJUNGgVlSTI47TMd5o0ARbH5gY2jbb0uY35%2FfHjB9n8NxNtf5EFVG881CPtrE%2Fq%2FnQTwN7VgExLwKCsQE31efJX1AI8VuTJRgPhGvhxSUEXU0hTsCSNTqMU9yKZUQF7bIqO%2Fv6Wz45leV%2BiRH%2FEUVORqbkE6f1rn13YQ5bURXx34oHfQD%2FOyMKQ0dxtILynhCN70BSgQMAQqEu9r4W6BH0HKtbBvL0CuyeCijURE9MHyme6FTCNoYO%2BBjqwAd%2F4wvBhiogJBrroHQTEYCMpzr6xYdGSyrTZX%2FJ4xLF%2FFh3t60JbpK0gnrbR%2BxyaTXr%2FnpxmhdbQtlIwozJE0D4j4c1pkiX8aRXni8HU08utwPI3IzsULFgpkYP5Ycqgnk0iUQv5T7oQ03mYVF%2BsAaq3slXjXbl%2FAqm8a7N%2BkwhYM023uQiDC2opXw%2FiYSFNLe2%2BztYqw%2FOcAX2Nzklbpo08KkFBRL%2B2oPEf7tcpz3J0&X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Date=20250227T213636Z&X-Amz-SignedHeaders=host&X-Amz-Expires=300&X-Amz-Credential=ASIAQ3PHCVTYTN2A6TH3%2F20250227%2Fus-east-1%2Fs3%2Faws4_request&X-Amz-Signature=4bb717bcd83fb0b6e22094dd047ab066e0291eab29970fcec68c2fa02e7684fc&hash=9b2a99f879d1b4d0a63ea33e76443ff8e186aaeaaac56a9a61ee433d254c5b44&host=68042c943591013ac2b2430a89b270f6af2c76d8dfd086a07176afe7c76c2c61&pii=0304397595001824&tid=spdf-8c22af76-e505-42b3-bda5-95de7ad03e1c&sid=278d522e3d66a9482f0a7aa63b840516ba7egxrqb&type=client&tsoh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&rh=d3d3LnNjaWVuY2VkaXJlY3QuY29t&ua=17135d53570353010252&rr=918b4fb58db10a18&cc=ru)
