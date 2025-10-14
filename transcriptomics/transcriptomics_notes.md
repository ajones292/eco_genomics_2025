## Transcriptomics Module

This is a place for me to keep my notes on my electronic/server activities during the transcriptomics module.

### 10/07/25

Learned about the motivation and process of asking questions and analyzing RNA-Seq data.

We started to run fastp to clean and visualize the data quality in our fastq files, but ran into file recognition issues in the custom script:

`~/projects/eco_genomics_2025/transcriptomics/myscripts/fastp_tonsa.sh`

### 10/09/25

Fixed file recognition issues in `fastp_tonsa.sh` by reformatting variables and created new output directory in `myresults`:

`~/projects/eco_genomics_2025/transcriptomics/myresults/fastp_reports/`

Viewed generated html files in `fastp_resports/` for the results of the cleaning and trimming processes.

Mapped C4 sample cleaned reads to reference genome using custom Salmon script:

`~/projects/eco_genomics_2025/transcriptomics/myscripts/salmon_quant.sh`

Permission errors caused by multiple users editing the C4 samples prevented Salmon from running.

### 10/14/25

Reviewed mapping rates and saved a mapping rate file:

`~/projects/eco_genomics_2025/transcriptomics/myresults/mapping_rate.txt`

Discussed sub-optimal mapping rates in most samples (~40%). There may be contamination of reads from other taxa that would not map to the reference transcriptome or low RNA yield/quality.

Could try head cropping while cleaning the reads in the event that that primers affected the mapping rate. We could also make a new *de novo* assembly from these reads

Prepared `quant.sf` files to be imported into DESeq2 and created a counts matrix with a custom R script:

`~/projects/eco_genomics_2025/transcriptomics/myscripts/create_counts_matrix.R`

Saved `counts_matrix.txt` to `mydata`:

`~/projects/eco_genomics_2025/transcriptomics/mydata/counts_matrix.txt`

Copied `metadata.txt` to `mydata`:

`~/projects/eco_genomics_2025/transcriptomics/mydata/metadata.txt`

Created an RMarkdown file to analyze and annotate the DESeq2 differential gene expression analysis:

`~/projects/eco_genomics_2025/transcriptomics/mydocs/DESeq2_notes.Rmd`

Average mapped reads in each sample (around 12 million) is below the general threshold recommendation of 20 million.

The variability in read number between samples will be accounted for as the individual size factors by DESeq2.

There is an average of around 2500 of reads mapped to each transcript. The median value for mapped reads is 19.

Histogram of read mapping shows that there are a couple million reads being mapped to a few transcripts.

Run DESeq2 to test for differential gene expression. Filter out genes with too few reads by removing all genes with counts < 15 in 18 samples.