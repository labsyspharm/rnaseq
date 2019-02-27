# Reference Genome {#refgenome}

* Navigate to `ftp://ftp.ensembl.org/pub/` and identify the latest release of the Ensembl reference genomes. As of writing this guide, the latest is `release-95`.
* For a given release, you will want to identify a `cdna` and a `gtf` file for your species. For example, when working with human data, the files are
  * `ftp://ftp.ensembl.org/pub/release-95/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz` and
  * `ftp://ftp.ensembl.org/pub/release-95/gtf/homo_sapiens/Homo_sapiens.GRCh38.95.gtf.gz`
* Ensure that you are in the `reference/` subfolder of your project.
* Download the reference files using the `wget` command:
  * `wget ftp://ftp.ensembl.org/pub/release-95/fasta/homo_sapiens/cdna/Homo_sapiens.GRCh38.cdna.all.fa.gz`
  * `wget ftp://ftp.ensembl.org/pub/release-95/gtf/homo_sapiens/Homo_sapiens.GRCh38.95.gtf.gz`
* If you are interested in also looking at the non-coding regions, you will want to download the matching `ncrna` file. Following the `release-95` example above, the download command will be
  * `wget ftp://ftp.ensembl.org/pub/release-95/fasta/homo_sapiens/ncrna/Homo_sapiens.GRCh38.ncrna.fa.gz`
  * After downloading both `cdna` and `ncrna`, merge the two together into a single file:
    * `cat Homo_sapiens.GRCh38.cdna.all.fa.gz Homo_sapiens.GRCh38.ncrna.fa.gz > Homo_sapiens.GRCh38.95.fa.gz`
