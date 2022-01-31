<!-- Copyright (C) 2021 by Jinwen XU -->

# crefthe - cross referencing with proper definite articles

"crefthe" is a LaTeX package aimed at helping `\cref` addressing the definite articles properly (especially for the article contractions in many European languages).

## Motivation

By default, when using cleveref's `\cref` to reference theorem-like environments, the names do not contain definite articles. This may be acceptable for English, but certainly not good enough for languages such as French, Italian, Portuguese, Spanish, etc. -- in these cases there shall be grammatical errors and would give you a strong feeling that it is machine-generated.

As an example, if we define the French names to be:
```latex
\crefname{theorem}{le théorème}{les théorèmes}
\crefname{proposition}{la proposition}{les propositions}
```
Then when one writes (which means "*We can deduce this from ...*"):
```latex
On peut le déduire de \cref{thm1,thm2,prop3}.
```
the result would be:
> On peut le déduire **de les** théorèmes 1 et 2 et **la** proposition 3.

which is wrong, as the correct result should be:
> On peut le déduire **des** théorèmes 1 et 2 et **de la** proposition 3.

`\cref` would not be able to handle such cases correctly.

## The solution

Thus, it would be better to have a new command `\crefthe[<prep>]{<labels>}`, and to use it like
```latex
\crefthe[de]{thm1,thm2,prop3}
```
in order to get "*des théorèmes 1 et 2 et de la proposition 3*".

# Usage

Simply load the package with:
```latex
\usepackage{crefthe}
```
> "crefthe" uses "cleveref" internally, thus it should usually be placed at the last of your preamble.

Before everything, you need to define the names, which can be done with `\crefthename`. Its syntax is similar to `\crefname`, but now you can specify the definite articles, for example:
```latex
\crefthename{theorem}[le]{théorème}[les]{théorèmes}
```

Then you can use the command `\crefthe` as follows:
- `\crefthe[<prep>]{<labels>}`
   - This will pass the preposition `<prep>` to the definite articles that follows. Its behavior depends on the current language (for example, in Spanish, `<prep>` is passed only to the first definite article, while in French it is passed to everyone).
- `\crefthe-[<prep>]{<labels>}` and `\crefthe+[<prep>]{<labels>}`
   - In case the automatic version does not meet your needs, here are two manual ones. The `-` version passes the preposition `<prep>` only to the first definite article, while the `+` version passes `<prep>` to every definite article.

> There is also a stared version `\crefthe*` for generating the same text but without hyperlinks.

*For more information, please refer to its documentation.*

# License

This work is released under the LaTeX Project Public License, v1.3c or later.
