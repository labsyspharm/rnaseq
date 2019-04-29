# Laboratory of Systems Pharmacology - RNAseq

Guide for aligning deep RNAseq and Digital Gene Expression (DGE) reads using bcbio: https://labsyspharm.github.io/rnaseq

The guide is built automatically by Travis-CI, with the end result served from `gh-pages` branch. If desired, the guide can be also be compiled locally using the `bookdown` package in R:
```
if( !require(bookdown) ) install.packages("bookdown")
bookdown::render_book("index.md")
```
