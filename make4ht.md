# Make4ht



## About

[`make4ht`](https://ctan.org/pkg/make4ht) is a system for producing HTML files from LaTeX input.

- [PDF documentation](http://mirror.utexas.edu/ctan/support/make4ht/make4ht-doc.pdf)
- [TUG article](http://www.tug.org/TUGboat/tb40-1/tb124hoftich-make4ht.pdf) : Somewhat technical; it is from the TeX user group journal, after all
- [Cheat sheet](https://www.12000.org/my_notes/faq/LATEX/htch4.htm) : Useful, if terse.

This document will show my steps working towards a solution with `make4ht`.

**Current summary:** It works on trivial examples, but throwing a large (but utterly standard) bit of LaTeX at it produces some horrible HTML output.


## Minimal working example

A very simple example, to check things work.  The [LaTeX file](sources/make4ht%20project%201/main.tex) is vanilla LaTeX.  We run the command

    make4ht main.tex "htm,mathjax"

(On Windows, using MikTeX, I had to install some additional packages, which happens automatically, if slowly.)  We should find `main.htm`.  Open this is a web browser, and you should see the expected output.  Right click on the displayed formula to see the MathJax context menu.

- You can see the [HTML output here](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%201/main.htm).

An alternative is to run

    make4ht main.tex "htm,mathml"

This produces an HTML file with [MathML](https://en.wikipedia.org/wiki/Mathml) used to represent the formulae.  These will be displayed correctly in Firefox, but not in Chrome, for example.  Instead, we copy and paste the MathJax `<script>` elements from the 1st file to the 2nd, and now the maths will display.  Under the hood, the HTML document no longer contains readable TeX fragments, but instead rather unreadable MathML code.

- You can see the [HTML output here](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%201/main_mathml.htm).

### Screen reader results

Results from [screen reader tests](mathjax.md):

- ChromeVox can read the MathJax generated formulae.
- ChromeVox can read the MathML formulae, but _only_ if Accessibility -> Assistive MathML is selected in the MathJax context menu.  Otherwise formulae are ignored.
- NVDA (with caveats) copes with both forms, but again _only_ is the Assistive MathML option is enabled.

### MathJax v3

We can also manually switch out MathJax v2 for MathJax v3, by editing the HTML files.  If you are using the "minimal" versions of the scripts, remember to choose the correct one; for example, for MathML input, use

    <script type="text/javascript" id="MathJax-script" async src="https://cdn.jsdelivr.net/npm/mathjax@3/es5/mml-chtml.js"></script>

The [TeX input example](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%201/mainv3.htm) and [MathML input example](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%201/main_mathmlv3.htm) can be viewed.  Results from [screen reader tests](mathjax.md):

- You _must_ have Accessibility -> Activate turned on.
- If you _click_ on the formula with ChromeVox, it is read.  However, when navigating around the document, the formulae are skipped.  Same result for TeX or MathML input.
- NVDA works exactly as in v2; and now whether Accessibility -> Activate is turned on or not doesn't seem to matter.
- The words spoken are subtly different between v2 and v3.  For example, the LaTeX $f:z\mapsto z^2+5$ is spoken as "f ratio ..." in v2, and "f colon ..." in v3.  The latter is probably better; of course in a lecture I would say "f is a map sending z to z squared plus 5", and it is a skill students will develop to make this sort of translation from _symbols_ to _meaning_.


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

  Unfortunately, when I try this I get a number of errors from `htlatex`: these do not contain sufficient information to allow me to see what is happening.  The [output](https://matthewdaws.github.io/AccessibleLaTeX/make4ht%20project%203/main.html) however seems correct, though I have not checked it closely.
  
  The mathematics is rendered correctly now.

- You can split the output into more than one html file, based upon the LaTeX sections, by using

      make4ht -u main.tex "htm,2,mathjax,charset=utf-8"

  Here I also add some commands to try to get [utf-8](https://en.wikipedia.org/wiki/UTF-8) support.  This would be nicer for a long document.


### Quality of the output

While the output is visually pretty nice, under the hood things get pretty nasty.  I noticed this when my screen reader started saying odd thinks like "link" in the middle of a sentence.  Examining the HTML output shows why:

    <span 
    class="cmr-12">The classical Bohr Compactification of a topological (semi)group can be defined in terms of</span>
    <span 
    class="cmr-12">unitary representations (see the original paper of von Neumann </span><span class="cite"><span 
    class="cmr-12">[</span><a 
    href="#Xvn1"><span 
    class="cmr-12">29</span></a><span 
    class="cmr-12">]</span></span> <span 
    class="cmr-12">or see </span><span class="cite"><span 
    class="cmr-12">[</span><a 
    href="#XBJM"><span 
    class="cmr-12">2</span></a><span 
    class="cmr-12">, ???]</span></span> <span 
    class="cmr-12">for a modern</span>
    <span 
    class="cmr-12">treatment).

The `class="cmr-12"` is trying to apply a CSS rule (120% size).  I would write this as:

    <p>The classical Bohr Compactification of a topological (semi)group can be defined in terms of
    unitary representations (see the original paper of von Neumann <a href="#Xvn1">[29]</a> or see
    <a href="#XBJM">[2, ???]</a> for a modern treatment).

There is nothing strange in the input LaTeX file to suggest why many different `spans` would be produced.

It was suggested to me to use the [tidy](https://github.com/htacg/tidy-html5) programme on the output.  On Windows, you need to install this separately, e.g. [from here](http://www.paehl.com/open_source/?HTML_Tidy_for_HTML5).  However, this didn't do anything structural to the HTML code.

This is (almost) a breaking feature as far as I am concerned.  The whole principle behind accessibility is to produce rather minimal HTML code which has clearly defined semantic meaning, and then to use CSS to provide styling.  Then automated tools (like screen-readers) have an easier time understanding the structure of the document.
