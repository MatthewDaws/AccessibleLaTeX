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

- You can see the [HTML output here](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%201/main.htm).
- The _bad news_: On testing with ChromeVox, the mathematics is not really read at all.  More on this later.


## More complicated example

Here we use a (very old, stalled, partly complete) research paper of mine as an example.  The LaTeX is standard, but complicated.  There are theorem environments, custom commands etc.  We run the same command to `make4ht`.  The [input file](sources/make4ht%20project%202) is the same, and you can [view the HTML output here](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%202/main.htm).

- It works!
- The output is a single file.
- The footnotes are bizarrely placed as entirely separate HTML files
- Theorems and so forth look correct.
- It is immediately clear that my custom macros are not being picked up by MathJax.  My understanding of why this is: the conversion tool is not really "compiling" the mathematics in any sense, it is simply "cutting and pasting" the LaTeX code into the HTML, where MathJax can interpret it.  As such, it doesn't "know" that custom LaTeX commands are being used.  Furthermore, these commands are not copied either.  One solution would be to copy all the LaTeX commands over to the first LaTeX block in the HTML file: MathJax will read and process these, and all subsequent LaTeX blocks will be aware of the custom commands.

Some variations:

- In his [Talmo talk](http://talmo.uk/events.html) (Scroll to section "Chris Hughes: Accessibility in Maths and Stats") it was suggested to use MathML output with MathJax v3 to render this.  This can be elegantly accomplished by using a small "configuration" file, see the files in [Project 3 files](sources/make4ht%20project%203).  The command now is

      make4ht -c main.cfg main.tex

  Unfortunately, when I try this I get a number of errors from `htlatex`: these do not contain sufficient information to allow me to see what is happening.  The [output](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%203/main.htm) however seems correct, though I have not checked it closely.
  
  The mathematics is rendered correctly now.

- You can split the output into more than one html file, based upon the LaTeX sections, by using

      make4ht -u main.tex "htm,2,mathjax,charset=utf-8"

  Here I also add some commands to try to get [utf-8](https://en.wikipedia.org/wiki/UTF-8) support.  This would be nicer for a long document.

