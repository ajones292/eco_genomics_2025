# Final Project Notebook

## Fall 2025 Ecological Genomics

## Author: Aidan Jones

This will keep my notes on my contributions to the final project

### Mapping Reference Transcriptome to Reference Transcriptome

Genes from the *Acartia tonsa* reference transcriptome were mapped to the indexed reference genome using Minimap2:

`~/projects/eco_genomics_2025/final_project/myscripts/tonsa_mapping.sh`

The alignment SAM file was processed using sambamba to convert the output to a BAM format. Alignment coordinates were sorted and the BAM file was indexed before bedtools was used to convert it to BED format:

`~/projects/eco_genomics_2025/final_project/myscripts/tonsa_process_bam.sh`

The resultant BED file containing the genomic coordinates of the reference genes will be used for downstream window-based enrichment analysis.

### Annotating Repetitive Elements in the Reference Genome

Repetitive DNA elements within the *Acartia tonsa* reference genome were identified and classified using RepeatMasker with a list of consensus sequences from the Dfam consortium:

`~/projects/eco_genomics_2025/final_project/myscripts/repeatmasker.sh`

Annotations were directed to a GFF format file such that genomic coordinates and families identifiers can be easily extracted for downstream window-based enrichment and motif scanning analyses.

### Heat Stres Treatment Differential Gene Expression Analysis

Created an R Markdown file for all further downstream analysis involved differential gene expression calculations and transposable element enrichment:

`~/projects/eco_genomics_2025/final_project/mydocs/TE_enrichment.Rmd`

Established DESeq2 contrast between the first generation of the control and treatment groups to extract genes involved in the initial head stress response.

### Transposable Element Proximity Enrichment Analysis

Filtered out structural elements and low-complexity regions from the RepeatMasker output to remove uninformative noise the may skew downstream analysis.

Used gene coordinates to create promoter-proximal windows for each gene by extending 5 kb upstream and including the full gene body.

Identified overlaps between these windows and transposon annotations and performed Fisher's exact test for each family.

### Transcription Factor Motif Scanning

Position frequency matrices of consensus insect transcription factor binding motifs were obtained from JASPAR:

`~/projects/eco_genomics_2025/final_project/mydata/MotifMatchr/JASPAR2026_CORE_insects_non-redundant_pfms_jaspar.txt`

Processed matrices and for scanning transposable element sequences of each enriched family with the R package motifmatchr.