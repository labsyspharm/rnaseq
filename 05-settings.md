# YAML Settings {#settings}

`bcbio` offers a rich suite of analysis tools, with [highly-customizable configurations](https://bcbio-nextgen.readthedocs.io/en/latest/contents/configuration.html#algorithm-parameters). The number of options can be overwhelming. Here, we provide exemplar files that should work for most analysis. These should serve as the starting point, and users are expected to tweak the files to suit their particular needs.

* For the purposes of consistency with the rest of the guide, please name your configuration file `O2.yaml`.
* If you downloaded and merged the reference for non-coding regions as [discussed previously](#refgenome), replace `GRCh38.cdna.all.fa.gz` with `GRCh38.95.fa.gz` in the examples below.
* In the YAML format, white space matters! When copying and pasting the examples below, please ensure that each line is properly indented.

## Digital Gene Expression

Copy and paste the following lines to your `O2.yaml`. Replace `abc123` with your eCommons ID and `myProject` with your project name.

```
details:
  - analysis: scRNA-seq
    algorithm:
      transcriptome_fasta: /n/scratch2/abc123/myProject/reference/Homo_sapiens.GRCh38.cdna.all.fa
      transcriptome_gtf: /n/scratch2/abc123/myProject/reference/Homo_sapiens.GRCh38.95.gtf
      umi_type: harvard-scrb
      minimum_barcode_depth: 0
      cellular_barcode_correction: 1
      positional_umi: False
    genome_build: hg38
```



## Deep RNAseq

Copy and paste the following lines to your `O2.yaml`. Replace `abc123` with your eCommons ID and `myProject` with your project name. Ensure that the Spike-in FASTA file matches what you [downloaded previously](#refgenome).

```
details:
  - analysis: RNA-seq
    genome_build: hg38
    algorithm:
      transcriptome_fasta: /n/scratch2/abc123/myProject/reference/Homo_sapiens.GRCh38.cdna.all.fa
      transcriptome_gtf: /n/scratch2/abc123/myProject/reference/Homo_sapiens.GRCh38.95.gtf
      aligner: hisat2
      strandedness: firststrand
      spikein_fasta:  /n/scratch2/abc123/myProject/reference/ERCC92/ERCC92.fa 
```
