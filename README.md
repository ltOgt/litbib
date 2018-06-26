# thebibliography
LaTeXs `\thebibliography` is easy to use and requires no extra compiler / more than two compile runs.

# *.bib
Bibtex and other bibliography management tools allow for the usage of bibliography files (`*.bib`),
in which fields can be specified to be assembled to a coherent style later on:
```
@article{einstein,
    author =       "Albert Einstein",
    title =        "{Zur Elektrodynamik bewegter K{\"o}rper}. ({German})
        [{On} the electrodynamics of moving bodies]",
    journal =      "Annalen der Physik",
    volume =       "322",
    number =       "10",
    pages =        "891--921",
    year =         "1905",
    DOI =          "http://dx.doi.org/10.1002/andp.19053221004"
}
```
(https://de.sharelatex.com/learn/Bibliography_management_with_bibtex)

This requires external compilers and multiple runs,
not to mention the complicated solutions for the integration of multiple bibliographies.

# litbib
With this package I tried to combine the best of both worlds.
You can specify `\lit` items with fields like in `*.bib` files,
but `\bibitems` are generated directly with their structure defined in the definition of the `\lit` command.
The style is based on APA but diverges somewhat.

Only the default compiler is required, and no more than the usual two complile runs are needed.

The integration of mutliple bibliographies is as easy as using the `\begin{litbib}[<optional name of bibliography>] ... \end{litbib}` environment at more than one place.

If you want continuous numbering just import the package with the option `crosscite`.

If you want to label the references yourself import the package with the `customlabel` option. Note that you will then need to define a label for each entry however. Automatic label creation is planned.

## how to use the package
Simply move the `litbib.sty` file in to the directory of your main latex file, or add it to your tex home directory (e.g. `~/texmf` on unix; run texhash to update the database).
You can then use it as any other package with `\usepackage` or `\RequirePackage`.

Instead of using `\thebibliography`, you use `\litib`.

Instead of using `\bibitem` , you use `\lit`, which takes a list of parameters and the reference label as arguments.

### Values
To specify the main text you cited use the following:
```
authors = n.a.,		% Authors
year = n.d.,		% Year published
title = n.t.,		% Title
volume =,		% Volume
issue =,		% Issue
isbn =,			% Isbn
doi =,			% doi
```
To specify the book / journal / ... the text is included in use: 
```
inEditors =,		% Editors of the larger work
inTitle =,		% Title of the book / journal / collection / ...
inYear =,		% Year of publication
inPages =,		% Pages on which the cited text can be found
inVolume =,		% Volume of the larger work
inIssue =,		% Issue
inIsbn =,		% Isbn
inDoi =,		% doi
```
To specify the publisher use:
```
pubLocation =,		% City / Country / ...
pubPublisher =,		% Company / Institution / ...
```
To specify e.g. an internet source use:
```
addInetSrc =,		% use with \protect\url{}
addInetDate =,
addNote =,
```

The only values that will always be used are `authors`,`date`,`title` (If not set: `n.a`,`n.d`,`n.t`).

For the book / journal / ... at least the title has to be set for any of its values to be included.

If ISBN is set, doi is ignored.

Titles are italic.

### example
```
\usepackage{litbib}
%\usepackage[crosscite]{litbib}
%\usepackage[customlabel]{litbib}

\begin{litbib}[Bibliography of Chapter 1]
			\lit{
				authors = {Turing, A.M.}, % If a value contains a comma, it needs to be surrounded with braces. 
				year = 1936,
				title = {On Computable Numbers, with an Application to the Entscheidungsproblem},
				inTitle = Proceedings of the London Mathematical Society,
				inVolume = 42,
				inIssue = 1,
				inYear = 1937,
				inPages = 230-265,
				inDoi = 10.1112/plms/s2-42.1.230,
				label = {Turing, 1936} % this will be ignored if the option "customlabel" is not set on import
			}{turing1936}
\end{litbib}
```
For the effects see the provided example files.

## style
As of now only one fixed style is provided, it is planned to provide more styles based on commonly used ones.
You can obviously also redefine the default one in the `litbib.sty`.

The APA based style can roughly be discribed the following way:
```
<AUTHORS> (<year>). <TITLE>.[ <IN>.][ <PUBLISHER>.][ <ADDITIONS>.]

<AUTHORS>   := <AUTHOR>[, <AUTHORS>]
<AUTHOR>    := <Last Name>, <First Name Initial>.

<TITLE>     := <title>[, (published <year>)][, <NUMBER>][ {(ISBN: <isbn>)|(DOI: <doi>)}]

<IN>        := In: [<AUTHORS>. ]<TITLE>
<NUMBER>    := [Vol. <volume_number>] [(<issue_number>)][, p.<first_page>-<last_page>]

<PUBLISHER> := [<city>, [<state>,] <country>. ]<publisher>

<ADDITIONS> := {<INTERNET>|<NOTE>}[, <ADDITIONS>]
<INTERNET>  := Retreived from: <url> "["<YYYY-MM-DD>"]"
<NOTE>      := Note: <remark>
```
Not everything is enforced and there might be some differences to the actual implementation (I will have to check again).

## what the package does
The package reads the provided values (via `xkeyval`) and generates a `\bibitem` with the values arranged and formated according to the style (using `ifthen`).

If all values are set the style generates:

`[LABEL] AUTHORS (YEAR). TITLE, Vol.VOLUME(ISSUE). ISBN: ISBN. In: INEDITORS
(Ed.), INTITLE, (published INYEAR), Vol.INVOLUME(INISSUE),
p.INPAGES. ISBN: INISBN. PUBLOCATION, PUBPUBLISHER.
Retreived from: INETSRC [INETDATE]`

(See `full_example`)

The package also provides a slightly adjusted environment (`\litbib` instead of `\thebibliography`) to change the title of the bibliography and handle continuous numbering (`crosscite` option).

You can also just use the `\lit` items in a regular `\thebibliography` environment, as normal `\bibitem`s are generated.

# TODO
`[ ]` Develop a little script to generate `\lit` items from existing `*.bib` files.

`[ ]` Provide multiple bibliography styles.

`[X]` Enable custom labels.

`[ ]` Generate custom labels based on style (e.g. APA from author and year)

`[ ]` Add note.

# Note
I don't really know what I am doing. Any feedback on how to do things better is greatly appreciated.

Also note that -- as I don't know what I am doing -- this package might not be usefull to you. The existing solutions offer a great amount of customizability and are -- with the `.bib` file -- the de facto standard. This solution was just something that fit my needs and I thought I might as well share it.
