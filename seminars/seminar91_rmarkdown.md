Markdown and R Markdown
=======================

Getting Started
===============

Open RStudio, and install the *knitr* package.

```r
install.packages('knitr')
```

Markdown
========

Markdown is a simple plain text markup language for formatting
documents. It's usually rendered to HTML, which is easy to view in a
web browser or to publish on the web. It can be rendered to other
document formats as well using a tool such as [Pandoc][pandoc].

- GitHub's [Markdown Basics][basics] describes the Markdown format
- GitHub has a few extensions to the Markdown syntax, called
  [GitHub Flavored Markdown][gfm]
- Daring Fireball, the creator of Markdown, gives a more detailed
  description of the [Markdown syntax][df]

Markdown documents have the file extension *.md*. This is the
canonical file extension. *Don't get creative here.*

[basics]: https://help.github.com/articles/markdown-basics
[gfm]: https://help.github.com/articles/github-flavored-markdown
[df]: http://daringfireball.net/projects/markdown/syntax
[pandoc]: http://johnmacfarlane.net/pandoc/

Example Markdown documents
--------------------------

GitHub automatically renders Markdown files with the *.md* extension.
Select *Raw* to view the raw Markdown.

- [A simple example][simplemarkdown], including a mathematical formula in LaTeX
- [This document][thisdocument]
- Open RStudio, and select *RStudio File > New File > R Markdown*.
  Ignore or delete the chunks of R code, for now.
- Find one on the Internet
- Write one for yourself!

[simplemarkdown]: https://github.com/jennybc/2013-11_sfu/blob/master/simple-markdown.md
[thisdocument]: https://github.com/jennybc/stat540_2014/blob/master/seminars/seminar91_rmarkdown.md

Rendering a Markdown document
-----------------------------

### RStudio

Open a Markdown document in RStudio. Click the *Preview* button.

Whenever you have a Markdown or R Markdown file open in the editor,
the button bar of the editor will have special powers. Click on the
question mark `?` to display the *Markdown Quick Reference* in the
*Help* panel.

### R command line

```r
library(markdown)
markdownToHTML('README.md', 'README.html')
```

### Shell command line

You can run R from the command line and call *markdown::markdownToHTML*.

```sh
Rscript -e 'markdown::markdownToHTML("README.md", "README.html")'
```

Alternatively on Mac OS, install the *markdown* program using
[Homebrew](http://brew.sh).

```sh
brew install markdown
markdown README.md >README.html
```

### Mac OS X

The [MOU](http://mouapp.com/) app shows a live preview of the
rendered document while you edit the markdown.

### Web browser extension

With the [Markdown Here](http://markdown-here.com/) browser extension,
you can write an e-mail (or Google Group posting, etc.) in Markdown
and render it before sending the e-mail.

R Markdown
==========

R Markdown intermingles documentation in Markdown format and chunks
of R code in fenced code blocks. When the R Markdown document is
*knit* (that is to say, compiled), the chunks of R code are run, and
the results, which can be text or figures, are inserted in the
rendered document. R Markdown documents have the file extension *.rmd*.

RStudio has some nice documentation on R Markdown.

- [Using R Markdown with RStudio][rstudiomd]
- [Equations in R Markdown][equations]

[rstudiomd]: http://www.rstudio.com/ide/docs/authoring/using_markdown
[equations]: http://www.rstudio.com/ide/docs/authoring/using_markdown_equations

Example R Markdown documents
----------------------------

- [A simple example][simplermarkdown]
- Open RStudio, and select *RStudio File > New File > R Markdown*.

GitHub does not render R Markdown documents automatically,
sadly.

[simplermarkdown]: https://github.com/jennybc/2013-11_sfu/blob/master/simple-r-markdown.rmd

Rendering a R Markdown document
-------------------------------

### RStudio

Open a R Markdown document in RStudio. Click the *Knit HTML* button.

### R command line

The R function *knit2html* first calls *knit* to generate a Markdown
file and then *markdownToHTML* to generate a HTML file.

```r
library(knitr)
knit2html('simple-r-markdown.rmd')
```

### Shell command line

You can run R from the command line and call *knitr::knit2html*.

```sh
Rscript -e 'knitr::knit2html("simple-r-markdown.rmd")'
```

A [Makefile][wikimake] is a good way of running a pipeline of multiple
R scripts and rendering the final report (in R Markdown, of course).
Here's an [example of a Makefile][rmdmakefile] for rendering R
Markdown.

[wikimake]: http://en.wikipedia.org/wiki/Make_(software)
[rmdmakefile]: https://github.com/jennybc/STAT545A/blob/master/hw06_scaffolds/03_knitWithoutRStudio/Makefile

Rendering a R script
--------------------

An R script can be rendered as though it were an R Markdown document
containing a single code chunk.

### RStudio

Open the R script in RStudio. Select *File -> Compile Notebook*.

### R command line

The R function *stitch_rmd* does something very similar to *File -> Compile Notebook*.

```r
library(knitr)
stitch_rmd('an-r-script.r')
```

### Shell command line

You can run R from the command line and call *knitr::stitch_rmd*.

```sh
Rscript -e 'knitr::stitch_rmd("an-r-script.r")'
```

Publishing a R Markdown document on RPubs
-----------------------------------------

RMarkdown documents can be published and shared on [RPubs][rpubs].

- Create an account on [RPubs][rpubs]
- Open the RMarkdown file in RStudio
- Click the *Knit HTML* butotn
- Click the *Publish* button

RPubs publishes the rendered document, but sadly does not also publish
the raw R Markdown code. The *rmd* file can be published on
[GitHub](github) or as a [GitHub gist](gist).

[rpubs]: http://rpubs.com
[github]: https://github.com
[gist]: https://gist.github.com

### Windows SSL certificate problem

Windows users may run into an SSL certificate problem when first attempting to upload to RPubs. Here is advice developed by the long suffering students in STAT 545A:

- Your basic solution can be found [here](http://support.rstudio.org/help/discussions/problems/2513-problem-with-publish-to-rpubs-windows-rstudio-096231)
- You will need to add the line `options(rpubs.upload.method = "internal")` to the file `Rprofile.site` which will live somewhere like this: `C:\Program Files\R\R-3.0.1\etc`. Yes take the `etc` __literally__. There is a directory with this name.
- You will need administrator access to edit this file, which you can get by right licking and choosing "Run as administrator" when you launch whatever you're going to use for editing.
- Do not edit something like this with (eeeeekkk) Word. Use Notepad or even the RStudio editor. Plain text editing!
- Another way to get permission to edit this file: Right click on the file, choose "Properties"--> "Security", and Edit to give "Full control" to "Users". Then you will be given the permission to edit the file.

Further Reading
===============

+ Carson Sievert's talk [Reproducible web documents with R, knitr & Markdown](http://cpsievert.github.io/slides/markdown/)
+ [MathJax](http://www.mathjax.org) is an open source JavaScript
  display engine for mathematics that works in all browsers ... It just
  works
+ Jeromy Anglim's blog post [Getting Started with R Markdown, knitr, and Rstudio 0.96](http://jeromyanglim.blogspot.ca/2012/05/getting-started-with-r-markdown-knitr.html)
  and a [Gist containing the source](https://gist.github.com/jeromyanglim/2716336)
+ Yihui Xie [blog post](http://yihui.name/en/2013/10/markdown-or-latex/)
  about when to use Markdown and when to use LaTeX
+ How to change the CSS used when R markdown is converted to HTML
  - [Step-by-step instructions](http://www.stat.ubc.ca/~jenny/STAT545A/topic10_tablesCSS.html)
    from Jenny Bryan's STAT 545A course
  - [Customizing Markdown Rendering](http://www.rstudio.com/ide/docs/authoring/markdown_custom_rendering)
+ Ben Bolker RPub [Literate programming, version control, reproducible research, collaboration, and all that](http://rpubs.com/bbolker/3153)
