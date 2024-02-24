<!-- Copyright (C) 2021-2024 by Jinwen XU -->

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

### The solution

Thus, it would be better to have a new command `\crefthe[<prep>]{<labels>}`, and to use it like
```latex
\crefthe[de]{thm1,thm2,prop3}
```
in order to get "*des théorèmes 1 et 2 et de la proposition 3*".

## Usage

Simply load the package with:
```latex
\usepackage{crefthe}
```
> "crefthe" uses "cleveref" internally, thus it should usually be placed at the last of your preamble.

> With the package option `overwrite`, you may simply use `\cref` for `\crefthe`, and similarly for other commands.

Before everything, you need to define the names, which can be done with `\crefthename`. Its syntax is similar to `\crefname`, but now you can specify the definite articles, for example (in French):
```latex
\crefthename{theorem}[le]{théorème}[les]{théorèmes}
```

Then you can use the command `\crefthe` as follows:
- `\crefthe[<prep>]{<labels>}`
   - This will pass the preposition `<prep>` to the definite articles that follows. Its behavior depends on the current language (for example, in Spanish, `<prep>` is passed only to the first definite article, while in French it is passed to everyone).
- `\crefthe-[<prep>]{<labels>}` and `\crefthe+[<prep>]{<labels>}`
   - In case the automatic version does not meet your needs, here are two manual ones. The `-` version passes the preposition `<prep>` only to the first definite article, while the `+` version passes `<prep>` to every definite article.

> - There is also a stared version `\crefthe*` for generating the same text but without hyperlinks.
> - The name-only relatives are also available: `\namecrefthe` and `\namecrefsthe`.
> - `\cpagerefthe` and `\Cpagerefthe` are provided as well.

### Regarding language with declensions

In German, there are four declensions: nominative (`Nominativ`), genitive (`Genitiv`), dative (`Dativ`) and accusative (`Akkusativ`). For such situation, we introduce the command `\crefthevariantname` to specify the referencing name for the correspond environment. Below is an example of usage:
```latex
\crefthevariantname{theorem}
  {
    {Satz}{Sätze}
    , Nominativ = [der]{Satz}[die]{Sätze}
    , Genitiv   = [des]{Satzes}[der]{Sätze}
    , Dativ     = [dem]{Satz}[den]{Sätzen}
    , Akkusativ = [den]{Satz}[die]{Sätze}
  }
```
The first line in the configuration is the default set of names when no variant is specified. It is recommended, though not required.

After this, you may refer to a theorem via

```latex
\crefthe[<prep>,variant=<declension>]{<label>}
```

You may also use the shortcuts (`nom.`, `gen.`, `dat.` and `akk.`), such as:

```latex
\crefthe[<prep>,Nom]{<label>}     \crefthe[<prep>,Nom.]{<label>}
\crefthe[<prep>,nom]{<label>}     \crefthe[<prep>,nom.]{<label>}
```

These four are all equivalent and you may choose one to use according to your preference.

> *For more information, please refer to the documentation.*

## Acknowledgement

There are so many people I wish to express my gratitude to during the development of this package, including:

- Patrick Bideault, without whose advice and careful explanation, this package probably would never have been born. Merci !

- Enrico Gregorio, Phelype Oleinik and Joseph Wright (in alphabetical order). They made valuable suggestions in the early development of this package and even edited some of the code themselves.

- Jonathan P. Spratte, without whose help the German support would probably take much longer to complete.

## License

This work is released under the LaTeX Project Public License, v1.3c or later.
