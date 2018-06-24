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
The style is in based on APA but diverges somewhat.

Only the default compler is required, and no more than the usual two complileruns are needed.

The integration of mutliple bibliographies is as easy as using the `\begin{litbib}[<optional name of bibliography>] ... \end{litbib}` environment at more than one place.
If you want continuous numbering just import the package with the option `crosscite`.

# TODO
The plan is to develop a little script to generate `\lit` items from existing `*.bib` files,
as well as the provision of more bibliography styles.
