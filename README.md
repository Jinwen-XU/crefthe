<!-- Copyright (C) 2021 by Jinwen XU -->

# ccref - cross referencing with proper definite articles

"ccref" is a LaTeX package aimed at helping `\cref` addressing the definite articles properly (especially for the article contractions in many European languages).

## Motivation

By default, when using cleveref's `\cref` to reference theorem-like environments, the names do not contain definite articles. This may be acceptable for English, but certainly not good enough for languages such as French, Italian, Portuguese, Spanish, etc. -- in these cases there shall be grammatical errors and would give you a strong feeling that it is machine-generated.

As an example, if we define the French names to be:
```latex
\crefname{theorem}{le théorème}{les théorème}
\crefname{proposition}{la proposition}{les propositions}
```
Then when one writes
```latex
On peut le déduire de \cref{thm1,thm2,prop3}.
```
(which means "*We can deduce this from ...*") the result would be
> On peut le déduire **de les** théorèmes 1 et 2 et **la** proposition 3.

which is wrong, as the correct result should be:
> On peut le déduire **des** théorèmes 1 et 2 et **de la** proposition 3.

`\cref` would not be able to handle such cases correctly.

## The solution

Thus, it would be better to have a new command `\ccref[<prep>]{<labels>}`, and to use it like
```
\ccref*[de]{thm1,thm2,prop3}
```
in order to get "*des théorèmes 1 et 2 et de la proposition 3*".
> The asterisk `*` here indicates that the preposition "de" will act on every definite article.

# Usage

Just load the package with
```latex
\usepackage{ccref}
```
> "ccref" uses "cleveref" internally, thus it should usually be placed at the last of your preamble.

And then you can use the command `\ccref` as follows:
 - `\ccref[<prep>]{<labels>}`
    - This will pass the `<prep>` to the first definite article.
 - `\ccref*[<prep>]{<labels>}`
    - This will pass the `<prep>` to every definite article.

However, before using it, you should first define the `\crefname`s carefully. The definite article in `\crefname`s needs to be marked manually using `\ccmarkart`, for example:
```latex
\crefname{theorem}{\ccmarkart{le} théorème}{\ccmarkart{les} théorème}
```


# License

This work is released under the LaTeX Project Public License, v1.3c or later.
