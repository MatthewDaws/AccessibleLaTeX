# Make4ht



## About

[`make4ht`](https://ctan.org/pkg/make4ht) is a system for producing HTML files from LaTeX input.

- [PDF documentation](http://mirror.utexas.edu/ctan/support/make4ht/make4ht-doc.pdf)
- [TUG article](http://www.tug.org/TUGboat/tb40-1/tb124hoftich-make4ht.pdf) : Somewhat technical; it is from the TeX user group journal, after all
- [Cheat sheet](https://www.12000.org/my_notes/faq/LATEX/htch4.htm) : Useful, if terse.

This document will show my steps working towards a solution with `make4ht`.  I intend later to add a guide to a final working solution, should one arise.


## Minimal working example

A very simple example, to check things work.  The [LaTeX file](sources/make4ht%20project%201/main.tex) is vanilla LaTeX.  We run the command

    make4ht main.tex "htm,mathjax"

(On Windows, using MikTeX, I had to install some additional packages, which happens automatically, if slowly.)  We should find `main.htm`.  Open this is a web browser, and you should see the expected output.  Right click on the displayed formula to see the MathJax context menu.

- You can see the [HTML output here](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%201/main.hhm).
- The _bad news_: On testing with ChromeVox, the mathematics is not really read at all.  More on this later.


## More complicated example

Here we use a (very old, stalled, partly complete) research paper of mine as an example.  The LaTeX is standard, but complicated.  There are theorem environments, custom commands etc.

