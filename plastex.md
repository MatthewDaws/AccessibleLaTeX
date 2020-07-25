# plasTeX

I haven't play with this extensively, but it seems to work.  [plasTeX]() is a LaTeX interpreter written purely in Python.  This means that you need a Python(3) installation, and a little fluency with Python.

I use [Anaconda Python](https://www.anaconda.com/products/individual) on Windows.

1. Use `pip` to install: `pip install plasTeX`  (case matters!)
2. The command-line script is copied to `Anaconda3\scripts\plastex` wherever your `Anaconda3` install is.  This won't run on Windows (there needs to be small `.exe` helper, I think).  Get around this by copying this script to wherever your LaTeX file is, and add the extension `.py` as you do this.
3. Now run `python plastex.py --renderer=HTML5 --dollars main.tex`
4. This will generate a directory `main` and a number of files beneath this.

**Unfortunately** the `pip` version is slightly out of date, in particular, contains a broken link to MathJax (which will fail if you try to serve the html code from an external web server: it must be `https`).  This can be fixed by installing the github version:

    git clone https://github.com/plastex/plastex
    cd plastex
    python setup.py install

You can see what the output looks like in the [official documentation](http://plastex.github.io/plastex/plastex/sec-config-html5.html).  However, none of the icons work for me (this seems to be a problem running locally: it looks okay on an external server.  As we are using Python, remember that you can run a simple webserver with `python -m http.server` and then navigate to `http://localhost:8000`.  This fixed the icons.)


### Example

On my more complicated example, I think I prefer the output to that given by `make4ht`.  The only wrinkle is the following error:

    WARNING: No Python version of latexsym.sty was found

This isn't so hard to fix, as `amssymb.sty` _is_ supported, and you can find most useful symbols there.

On the plus side, the custom math commands are handled completely transparently, which is a big win over `make4ht`.  Checking the output, what has happened is that the custom LaTeX commands have been expanded into vanilla LaTeX.  (I wonder if this is a complete win for accessibility?  I can imagine that a Mathematics student who used a screen-reader extensively will probably be a good LaTeX user, somewhat of necessity.  Imagine some lectures notes on complex analysis: would $\C$ or $\mathbb{C}$ be easier for the student?)

If you are happy with the steps given above, this is a pretty nice out of the box solution.  For research papers, the error about missing `xy.sty` will be much more annoying, but perhaps the people at [The Gerby Project](https://gerby-project.github.io/) have a work-around or fix.

You can see [some example output here](https://matthewdaws.github.io/AccessibleLaTeX/plastex/index.html).

## Todo

- Work out how the templating system works
- Come up with a nicer theme.  It is a "responsive" design, but the table of contents just disappears, which is far from elegant.
