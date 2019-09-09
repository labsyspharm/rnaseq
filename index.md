---
title: "Aligning deep RNAseq and Digital Gene Expression (DGE) reads using bcbio"
author: |
  | Artem Sokolov, Sarah Boswell, Jeremy Muhlich, Clemens Hug
  | Laboratory of Systems Pharmacology
date: "Last Updated: `r Sys.Date()`"
site: bookdown::bookdown_site
output: bookdown::gitbook
github-repo: labsyspharm/rnaseq
---

# Quick Start {-}

1. [Ensure your O2 environment is properly setup to run `bcbio`.](#prereqs)
2. [Put your data in permanent storage and create a copy on `/n/scratch2/`.](#data)
3. [Do you have multiple fastq files that need to be merged for each sample?](#sampledesc)
    - If yes, run `bcbio_prepare_samples.py` to merge the files. Rename the resulting `*-merged.csv` to `alignment.csv`. (This is often the case for deep RNAseq experiments.)
	- If not, compose `alignment.csv` that maps filenames to corresponding sample descriptions. (This is often the case for DGE.)
4. [(Optional) Download the latest human (or mouse) genome reference.](#refgenome)
5. [Compose a setting YAML file.](#settings)
6. [Instantiate the `bcbio` workspace. Descend into `alignment/work` subdirectory. Kick off a `bcbio` run.](#bcbio)

## Recommended Directory Structure {-}

To keep things organized, we recommend maintaining the following directory structure. Let `/n/scratch2/abc123/myProject/` be the root directory of your analysis. Replace `abc123` with your eCommons ID, and `myProject` with your project name. See the [section on data storage](#data) to learn how to create a copy of your data on `/n/scratch2`.

Under `/n/scratch2/abc123/myProject/` create the following subdirectories:

* `fastq` - place your raw fastq files here.
* `merged` - automatically created by `bcbio_prepare_samples.py` if you have [mulitple files per sample](#sampledesc-deep).
* `reference` - download your [reference genome](#refgenome) to this subdirectory.
* `alignment` - automatically created by `bcbio` together with its subdirectories:
    * `config` - `bcbio` will derive configuration files from your settings YAML file and place them here.
    * `work` - the bulk of the work files will reside here.
    * `final` - the resulting counts matrices will appear here, when `bcbio` finishes.
