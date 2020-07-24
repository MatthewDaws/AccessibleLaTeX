# Bookdown

[Bookdown](https://bookdown.org/home/about/) is an addon to [R Studio](https://rstudio.com/) which allows one to write books (or other, multi-part documents, which could be as short as a single talk) in [Markdown](https://en.wikipedia.org/wiki/Markdown) using LaTeX for maths.  The output can be compiled to HTML, PDF, Word, ePub etc.  This is somewhat less flexible than LaTeX proper, but (IMHO) the outputs often look visually nice.  As it seems that _any_ solution is likely to involve a lot of re-writing and testing, the cost of moving notes to new markup system is not that extreme.

## Installing

This unfortunately seems more painful than it should be (this whole thing feels like computing in 2005: I've been spoilt by things like Anaconda Python, or MikTeX, which _just work_.)

1. Download [R](https://www.stats.bris.ac.uk/R/) and install.
2. Download [RStudio](https://rstudio.com/products/rstudio/download/) and install.  (You need to also download R to get the latest version, as the copy bundled with RStudio is old.)
3. On Windows, you also need to download and install [RTools](https://cran.rstudio.com/bin/windows/Rtools/)
4. Also follow the steps to put "RTools on the path".  The easiest way to do this is to (re)start RStudio, and type

       writeLines('PATH="${RTOOLS40_HOME}\\usr\\bin;${PATH}"', con = "~/.Renviron")

   Restart RStudio again, and check that

       Sys.which("make")

    prints something like `"C:\\rtools40\\usr\\bin\\make.exe"`
5. Now type in the RStudio console

    install.packages("bookdown")

   This will take a while

6. Unfortunately, all this is probably incompatible with the hard-drive size of a Surface Pro.  I now have about 2.5Gb of new files on my computer.

Furthermore, R didn't seem to know about my MikTeX install.  I fixed this by manually editing the file `.Renviron` in my `Documents` directory, to be

    PATH="${RTOOLS40_HOME}\usr\bin;C:\Users\Matthew\AppData\Local\Programs\MiKTeX 2.9\miktex\bin\x64\;${PATH}"

You will need to alter `C:\Users\Matthew\AppData\Local\Programs\MiKTeX 2.9\miktex\bin\x64\` to be the path your MikTex install.


## First time project

1. In RStudio select File Menu -> New Project, then New Directory, then Book project using bookdown.
2. This will create a demo project for you.  Click on the "index.Rmd" file, and then select the "Knit" icon in that window.
3. Depending on the option you choose, for the 1st time, more R code will be downloaded and installed.
4. This will display _that section only_ in HTML format.
5. To build the whole book, select the `build` tab, and click on "build book".
6. Possibly you will get a PDFLaTeX error, or similar.  If so, I found that opening the "newbook.tex" file in your LaTeX system and compiling it will fix the errors. The file itself probably will not compile, but it will download all the extra LaTeX packages required.  Once these have been installed, RStudio seems happy enough compiling the PDF itself.  Note that the demo uses `XeLaTeX` not `PDFLaTeX`.

All this works, but it starts to look somewhat complicated.

