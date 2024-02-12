# (Optional) Reference Genome {#refgenome}

**This step is optional.** `bcbio` maintains a current version of human and mouse genomes internally. If you are happy with using the standard, proceed to [composing a setting YAML file](#settings). Otherwise, read on about composing a custom reference.

* Navigate to https://ftp.ensembl.org/pub/ and identify the desired release of the Ensembl reference genome. As of `r Sys.Date()`, the latest is `release-111`.
* For a given release, you will want to identify `cdna` and `gtf` files for your species. For example, when working with `release-111` human data, the files are

https://ftp.ensembl.org/pub/release-111/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz and
https://ftp.ensembl.org/pub/release-111/gtf/homo_sapiens/Homo_sapiens.GRCh38.111.gtf.gz

* Ensure that you are in the `reference/` subfolder of your project.
* Download the reference files using the `wget` command:

```
wget ftp://ftp.ensembl.org/pub/release-111/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz
wget ftp://ftp.ensembl.org/pub/release-111/gtf/homo_sapiens/Homo_sapiens.GRCh38.111.gtf.gz
```

* If you are interested in also looking at the non-coding regions, you will want to download the matching `ncrna` file. Following the `release-111` example above, the download command will be

```
wget ftp://ftp.ensembl.org/pub/release-111/fasta/homo_sapiens/ncrna/Homo_sapiens.GRCh38.ncrna.fa.gz
```

* After downloading both `cdna` and `ncrna`, merge the two together into a single file:

```
cat Homo_sapiens.GRCh38.cdna.all.fa.gz Homo_sapiens.GRCh38.ncrna.fa.gz > Homo_sapiens.GRCh38.111.fa.gz
```

* Unzip all files:

```
gunzip *.gz
```

## Digital Gene Expression

No additional steps required.

## Deep RNAseq {#spike-in}

When working with deep RNAseq data, you will also need to account for the [ERCC ExFold RNA Spike-In](https://www.thermofisher.com/order/catalog/product/4456739) that is often used for quality control.

* Determine the version of the spike in used in your experiment.
* Identify the FASTA file that catalogues spike-in sequences from the [vendor's page](https://www.thermofisher.com/order/catalog/product/4456739). This can usually be found under the manuals tab. As of writing this, ERCC92 is the latest version with the FASTA available at https://assets.thermofisher.com/TFS-Assets/LSG/manuals/ERCC92.zip
* Download the spike-in file to your `reference/` subdirectory:
```
wget https://assets.thermofisher.com/TFS-Assets/LSG/manuals/ERCC92.zip
```
* Unzip the downloaded file to retrieve the FASTA sequences: `unzip ERCC92.zip`
