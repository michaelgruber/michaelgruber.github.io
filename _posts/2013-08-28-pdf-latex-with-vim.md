---
layout: post
title: PDF LaTeX with Vim
subtitle: Never do the same thing more than a few hundred times.
---

![LaTeX User's Guide and Reference Manual Cover](http://media.tumblr.com/3d5d1d0c1df802ee5ff5ecbe6b9bf759/tumblr_inline_ms9vdt3ZK81qz4rgp.jpg) I’ve been in geek-love with two things recently: Vim and Markdown. I do all my note-taking and list-making with Markdown. And I'm totally head-over-heels for the [vim-instant-markdown](https://github.com/suan/vim-instant-markdown) plugin. Unfortunately, it just about spoiled me rotten when I had to whip together some LaTeX for the first time.

Sick of running `pdflatex` after any change, I cobbled together my first little Vim script to do the deed for me. TeX files are compiled on write, and the resulting PDF pops up in your default PDF viewer. Additionally, any writes to a `.cls` result in a search for TeX files referencing the class. Those files are PDF'd and opened as well.  It weighed in at only 32 lines but it did the trick, speeding up my annoying compile and check cycle nicely.

You can check out the source on [Github](https://github.com/michaelgruber/vim-latex-pdf).

Only after completing my little hobby project, I realized a similar plugin might already exist. That alternative seems to be [vim-latex-live-preview](https://github.com/xuhdev/vim-latex-live-preview). It's pretty nifty, but appears to require the use of [evince](https://projects.gnome.org/evince/) or [okular](http://okular.kde.org/) as pdf viewers, and also doesn't support multi-document files. So editing a `.cls` just gives me a `Failed to compile`.

Which makes my Vim project time well spent.