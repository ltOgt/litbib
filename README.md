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

## example
```
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
For the effects see the provided `book_example` and `article_example`, as well as `litbib.sty` for a complete list of available fields.

## style
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

# TODO
`[ ]` Develop a little script to generate `\lit` items from existing `*.bib` files.

`[ ]` Provide nultiple bibliography styles.

`[X]` Enable custom labels.

`[ ]` Generate custom labels based on style (e.g. APA from author and year)

# Note
I don't really know what I am doing. Any feedback on how to do things better is greatly appreciated.
