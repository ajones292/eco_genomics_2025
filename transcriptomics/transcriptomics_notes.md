## Transcriptomics Module

This is a place for me to keep my notes on my electronic/server activities during the transcriptomics module.

### 10/07/25

Learned about the motivation and process of asking questions and analyzing RNA-Seq data.

We started to run fastp to clean and visualize the data quality in our fastq files, but ran into file recognition issues in the custom script:

`~/projects/eco_genomics_2025/population_genomics/myscripts/fastp_tonsa.sh`

### 10/09/25

Fixed file recognition issues in `fastp_tonsa.sh` by reformatting variables and created new output directory in `myresults`:

`~/projects/eco_genomics_2025/population_genomics/myresults/fastp_reports/`

Viewed generated html files in `fastp_resports/` for the results of the cleaning and trimming processes.

Mapped C4 sample cleaned reads to reference genome using custom Salmon script:

`~/projects/eco_genomics_2025/population_genomics/myscripts/salmon_quant.sh`

Permission errors caused by multiple users editing the C4 samples prevented Salmon from running.