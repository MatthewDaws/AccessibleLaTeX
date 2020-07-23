# LaTeX hints and tips

Some random things I didn't know before:

### Working with subfiles

A common way of organising larger LaTeX project is to use multiple files: for example, one file per chapter, in a set of lecture notes.  Then a short `main.tex` file loads each subfile using the `\include` command.  I have tended not to use this structure, most recently because I use [TexWorks](http://www.tug.org/texworks/) which has no options to handle "projects", and so always tries to compile the currently open file.

(Why TexWorks?  It is rather feature-poor.  However, I like that!  I prefer having a simple text-editor, with spellcheck, and a simple tool chain.)

Turns out [there is a simple solution](https://tex.stackexchange.com/questions/377702/how-to-work-and-compile-efficiently-in-a-multi-file-project-in-texworks).  At the top of each sub-document you add

    %!TeX root=../thesis.tex

This example tells TexWorks, and other aware editors, that really the file `thesis.tex`, in a directory one level up, should be the file to compile.

TODO: How to work efficiently with very large documents: is it possible to compile only the current chapter, for example?


### Other editors

At some point, I should explore the LaTeX plugin for Visual Studio Code.
