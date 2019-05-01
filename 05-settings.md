# YAML Settings {#settings}

`bcbio` offers a rich suite of analysis tools, with [highly-customizable configurations](https://bcbio-nextgen.readthedocs.io/en/latest/contents/configuration.html#algorithm-parameters). The number of options can be overwhelming. Here, we provide exemplar files that should work for most standard analyses at the LSP. These should serve as a starting point, and users are expected to tweak the files to suit their particular needs.

* For the purposes of consistency with the rest of the guide, please name your configuration file `O2.yaml`
* If you downloaded and merged the reference for non-coding regions as [discussed previously](#refgenome), replace `GRCh38.cdna.all.fa.gz` with `GRCh38.95.fa.gz` in the examples below.
* In the YAML format, white space matters! When copying and pasting the examples below, please ensure that each line is properly indented.

## Digital Gene Expression

For DGE, we recommend to use the following configuration file as a template. Copy and paste the the lines below to your `O2.yaml` or [download it directly](example_settings/dge/O2.yaml) using the command `wget https://labsyspharm.github.io/rnaseq/example_settings/dge/O2.yaml`.

In the downloaded file, replace `abc123` with your eCommons ID and `myProject` with your project name.

```{r, dge, echo=FALSE, result="asis", comment=NA}
cat(
  paste(
    readLines(file.path("example_settings", "dge", "O2.yaml")),
    collapse = "\n"
  )
)
```

## Deep RNAseq

For deep RNAseq, we recommend to use the following configuration file as a template. Copy and paste the lines below to your `O2.yaml` or [download it directly](example_settings/rna_seq/O2.yaml) using the command `wget https://labsyspharm.github.io/rnaseq/example_settings/rna_seq/O2.yaml`.

In the downloaded file, replace `abc123` with your eCommons ID and `myProject` with your project name. Ensure that the Spike-in FASTA file matches what you [downloaded previously](#spike-in).

```{r, rna_seq, echo=FALSE, result="asis", comment=NA}
cat(
  paste(
    readLines(file.path("example_settings", "rna_seq", "O2.yaml")),
    collapse = "\n"
  )
)
```
