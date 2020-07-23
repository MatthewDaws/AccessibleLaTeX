# Motivation

I am now required by my university to make sure that all material available on our Virtual Learning Environment is "accessible", in the sense of [UK government legislation](https://www.legislation.gov.uk/uksi/2018/852/made).  These notes are written from the perspective of a lecturer interested in typesetting (pure) mathematics; I am not a lawyer, and while I have an interest in technology, I am not a professional software developer.  My initial aim is to give simple, workable solutions which might be useful to others.

[Matthew Towers's post](https://www.homepages.ucl.ac.uk/~ucahmto/elearning/latex/2019/05/06/accessibility-regulations.html) nicely sums up the issues.  His interpretation of the law accords well with what I have been told; neither of us are lawyers.


### Tools

My university, probably like many, works in the Microsoft ecosystem, and uses Blackboard.  Blackboard has the [Ally](https://www.blackboard.com/teaching-learning/accessibility-universal-design/blackboard-ally-lms) system for checking "accessibility".  The most recent versions of Microsoft Word, Powerpoint etc. are capable of producing accessible documents, and seemingly of converting these to PDF files.

By "accessible", in this context, we mostly mean screen readers (I only have access to [ChromeVox](http://www.chromevox.com/installing.html) for testing).  There is much more, of course, but it seems that standard software can accommodate well other issues (such as zooming).   We should also not forget the need to provide text alternatives for images, and so forth, but these matters are not "technical".

As a mathematician, I of course (I say this, but I am aware not all mathematicians work this way) only use LaTeX.  Here unfortunately the tools here are somewhat less developed.


### PDF files

My support material for teaching currently consists of many PDF files generated from LaTeX files (these vary, with some inherited from others lacking in formal structure, through to some notes which use nonstandard classes like the [Tufte](https://ctan.org/pkg/tufte-latex?lang=en) package) together with an unfortunately large number of handwritten documents.

PDF files are designed purely to represent a typeset document: "put this image here, but this text, in that font, over there".  There is little to no "internal structure": for example, a PDF reader cannot know that the large bold text here is meant to be a "heading" (and so have logical meaning), nor know what order to read text in.

PDF files support "tags" which can add this internal structure.  [Towers](https://www.homepages.ucl.ac.uk/~ucahmto/elearning/latex/2019/05/06/accessibility-regulations.html) describes various techniques to get LaTeX to produce tagged PDF files.  My experiences are:

- This doesn't convince Blackboard Ally: my PDFs go from being "poor" to "medium" accessibility
- The tools do not interact well with certain ways I write LaTeX (using dollar signs to delimit maths, for example) so there would still be a lot of manual work
- As Towers says, its far from clear if the generated PDF files really are "accessible", even if they pass some automated test.  In particular, are displayed formulae remotely comprehendible by screen readers?


### HTML

The approach suggested by Towers, and the only approach I have seen others suggest, is instead to convert LaTeX files to HTML and make use of [MathJax](https://www.mathjax.org/) to display the formulae.  MathJax is actually highly accessible; my quick tests with version 3 of MathJax and ChromeVox have been promising, with formulae read out in a Mathematically correct, sensible way.

HTML is also a good target for the reason that there are likely to be many tools which support it.  One imagines that a student who uses a screen reader will be adept at navigating webpages with it.  So, that's what I will pursue here: how to convert LaTeX documents into HTML.


### Other options

To look at in the future:

- [PreText](https://pretextbook.org/catalog.html) aka MathBook XML, the older name better reflecting what it does
- [BookDown](https://bookdown.org/) : LaTeX and Markdown, what's not to like?


### Resources

- [Towers](https://www.homepages.ucl.ac.uk/~ucahmto/elearning/latex/2019/05/06/accessibility-regulations.html) has a lot of interesting posts in this area: the linked post is a good place to start.
- [Talmo](http://talmo.uk/events.html) : Scroll down to Chris Hughes's presentation.
- [LMS page on accessibility](https://www.lms.ac.uk/policy/mathematics-and-accessibility) : Somewhat just another list.
