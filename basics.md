---
layout: default
title: "The S&P LaTeX system"
---

## Formats

While we accept submissions in both LaTeX and Microsoft Word formats, we publish all articles using LaTeX typesetting. We prefer LaTeX submissions, because it is easier to remain true to the author's vision when typeset in the S&P style and because it expedites the production process, thus leading to much faster publication. We therefore strongly encourage authors to submit in LaTeX format, and ideally in our house style. If you yourself are not familiar with LaTeX, maybe a friend or colleague could help you with preparing your manuscript. If you have to submit in Word format, please read our [Word-specific instructions](word).

## LaTeX configuration

Compiling in the S&P style requires two files, a TeX style file, [sp.cls](/source/sp.cls), and a BibTeX style file, [sp.bst](/source/sp.bst). (If you like to live on the cutting edge, replace sp.bst with [our BibLaTeX implementation of our bibliography style](https://github.com/semprag/biblatex-sp-unified).)

You can add these to your global TeX distribution, your local settings, or keep them in the same folder as your article.

On most Linux distributions, you can move these files to the following global paths:

    /texmf/tex/latex/sp.cls
    /texmf/bibtex/bst/sp.bst

On Mac OS X, with TeXLive, the files can be located at:

    ~/Library/texmf/tex/latex/local/sp.cls
    ~/Library/texmf/tex/latex/local/sp.bst

Having done that, you should now be able to get a document started by setting your document class:

    \documentclass{sp}

You will probably be better off starting from a minimal template, though, which includes sections for authors, abstract, keywords,
and many other required sections. You can download that file here: <a href="source/sp-template.tex">sp-template.tex</a>. Please consult [the detailed explanation of the template](basics).

*Semantics and Pragmatics* uses Lucida, a commercial font that is not freely redistributable.
The provided template uses Times, by default, but you can defer back to the LaTeX standard Computer Modern by specifying `\documentclass[cm]{sp}`.

## Style guidelines ##

In our experience, even submissions in LaTeX format often require intensive re-typesetting and additional work on the bibliography. We hope that authors can take some of the burden of that work, again in the interest of an expedited publication process. To that purpose, please read [our style guidelines](style), especially as they pertain to LaTeX submissions.

### Frontmatter (the preamble)

Instructions for the content that comes before `\begin{document}`.

#### Metadata

The `\pdf*{}` commands control the metadata inserted into the published PDF.
Only ASCII characters are allowed in these fields, otherwise the `pdflatex` compiler will throw very hard to debug errors.

#### Title

The `\title{}` can contain a `\thanks{}` acknowledgements section. If you do not give `\title[Something Short]{Full}` the optional argument (here, "Something Short"), no title will be shown in the headers of subsequent pages. If your title is shorter than 30 characters, use the same title for each.

#### Authors

There is no limit to the number of authors you can have. Each use of `\spauthor{}` should be separated by `\AND`.

The optional argument to `\author` (inside square brackets) is what appears in the header on subsequent pages. Just give your full name. For two authors, you can give both full names conjoined with *and*. When the author list becomes too long, use last names only, and use *&* instead of *and*. If you have more than three authors, use "Murphy et al." (where Murphy is the last name of the first author).

#### Keywords

The content of the `keywords` environment should be the same as the `\pdfkeywords{}` command, except that the environment allows an extended character set. Six is a good target for number of keywords.

## The document

### Examples

Our general formatting rules for examples:

- Example numbers appear in round parentheses, left-aligned.
- Subexamples are labeled with lowercase alphabetical letters, each followed by a period.
- Equations and examples should be numbered in the same sequence.
- References to examples appear inside parentheses, with no punctuation between elements.
  - E.g., we can refer to (12), or to its subexample (12a).

For simple needs, we have found that the [linguex package](http://www.ctan.org/pkg/linguex) works well with our style. You can load it by simply passing a `linguex` option to `sp.cls`.

For more complex needs (complex glosses, for example), we strongly recommend the [expex package](http://ctan.org/pkg/expex). We expect to offer full expex integration into our system soon.

We advise against all other example packages (gb4e, covington, etc.), because in our experience they create difficult integration problems with our house style.

### BibTeX and Citations

The `sp.cls` style file adds a few commands to the standard `natbib` commands. The `sb.bst` file will handle most details about how your `.bib` file is rendered, but here are a few things to keep in mind.

There are four main citation forms:

- `\citealt{montague:1974}`: Montague 1974
  - This refers to the work.
- `\citet{montague:1974}`: Montague (1974)
  - This refers to the author in the context of this work.
- `\citep{montague:1974}`: (Montague 1974)
  - This refers parenthetically to this work.
- `\citeauthor{montague:1974}`: Montague
  - Useful if you recently used `\citet{montague:1974}` and it's clear you're talking about the same work.

The S&P file also supports the following commands:

- `\pgcitealt{montague:1974}{12}`: Montague 1974: 12
- `\pgcitet{montague:1974}{12}`: Montague (1974: 12)
- `\pgcitep{montague:1974}{12}`: (Montague 1974: 12)
- `\seccitet{montague:1974}{2}`: Montague (1974: §2)
- `\posscitet{montague:1974}`: Montague's (1974)
- `\pgposscitet{montague:1974}{12}`: Montague's (1974: 12)
- `\possciteauthor{montague:1974}`: Montague's
- `\secposscitet{montague:1974}{2}`: Montague's (1974: §2)
- `\seccitealt{montague:1974}{2}`: Montague 1974: §2
- `\seccitep{montague:1974}{2}`: (Montague 1974: §2)

Every reference to an article must be coded with one of these commands.
This ensures that all bibliographic entries are included, and, since these automatically hyperlink to the corresponding entry in the bibliography, allows your readers to determine what work you are referring to.

### Images and custom figures

You can easily include a range of figures using the `\includegraphics{}` command.

    \includegraphics[width=4in]{figure-1b.pdf}
    \includegraphics[height=1in]{my-pet-cat.png}
    \includegraphics[width=\textwidth]{image-file.jpg}

N.B. `\includegraphics` prefers filenames without underscores.

### Floats, for figures and tables

The `sp.cls` includes the `float` package by default.
If you need to modify the S&P `float` configuration temporarily, you can:

    % outside brackets ensure that the style returns to normal
    % after the temporary adjustment
    {
      \floatstyle{plain}
      % See the `float` documentation for other styles.
      \restylefloat{figure}
      \begin{figure}
        \includegraphics{some-carefully-named.pdf}
        Your figure goes here.
      \end{figure}
    }

## Backmatter

The end sections are organized in this order:

1. Appendix
2. References
3. Addresses

### Appendix

The `appendix` environment, is a good home for lengthy proofs, fragments, experimental materials, etc.

    \begin{appendix}
      ...
    \end{appendix}

### References

Simply use the following, where you have a file `your-references.bib` in the same folder.

    \bibliography{your-references}

If you have a system-wide BibTeX file somewhere else that's accessible to your LaTeX library, that is fine too.
However, when submitting your article, you will need to include whatever `.bib` file you use here.

### Addresses

Full author addresses appear at the end of each article.
They are specified in an `addresses` environment, which consists of `address` environments:

    \begin{addresses}
      \begin{address}
        Author1 \\
        Street \\
        ... \\
        \email{author1@email.edu}
      \end{address}
      \begin{address}
        Author2 \\
        Street \\
        ... \\
        \email{author2@email.edu}
      \end{address}
      % repeat if needed
    \end{addresses}

## Packages included by sp.cls

The `sp.cls` file includes the following packages by default, which means you have access to all their commands without having to `\usepackage{}` it in your own document (in fact, it is a very good idea to delete the relevant `\usepackage{}` commands from your preamble):

- graphicx
- natbib
- hyperref
- amsmath
- amssymb
- float
- subfigure
- mathptmx
- stmaryrd
- textcomp
- microtype
- inputenc
- xspace
- ifthen
- color
- fontenc
- linguex (loaded by `[linguex]` package option)

## Postscript

We strongly recommend rendering directly to PDF with `pdflatex`, avoiding `dvi` and `ps` formats entirely.
This ensures that line breaks and hyperlinks appear correctly.

If you must use `postscript` for certain diagrams, we recommend rendering those to PDF format independently (e.g., via `latex` & `dvipdf` or by using `ps2pdf`), and then importing the result directly into your *S&P* submission:

    \includegraphics{used-to-be-ps.pdf}

Failing that, you can use the option `\documentclass[dvips]{sp}` or the `pdftricks` package.

If you provide us with a TeX document that requires postscript, we will most likely convert your figures to PDF and render the document with `pdflatex` anyway. By submitting in `pdflatex`-able format, with graphics in separate documents, you will ensure that the final publication is as close as possible to what you envision.
