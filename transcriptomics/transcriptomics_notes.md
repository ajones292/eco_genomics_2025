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

Run DESeq2 to test for differential gene expression. Filter out genes with too few reads by removing all genes with counts < 15 in 18 samples. Received a dataset with  14,566 genes.

### 10/16/25

Normalized counts data through variance stabilization to achieve approximately even expression across genes with different expression patterns.

Constructed a heatmap and cluster tree based on sample distance to determine the presence of outliers. There were no obvious outliers.

PCA revealed divergence of G1 and G2 from later generations in both control and treatment groups along PC1 (~32% variance). G1 in treatment groups in most diverged, but G2 moves closer towards the other control and treatment groups from later generations.

Tested for differential gene expression between treatments and generations through pairwise contrasts using the group model.

Assessed differential gene expression between control and treatment groups across all of the generations in the most 5 significant genes. For the most part, G2 in the control and treatment groups are going in opposite directions relative to G1, and coming back together in G3 and G4.

### 10/21/25

MA plot reveals there is a general trend of decreasing log-fold-change with increasing magnitude of expression.

Volcano plots showed there was is a positive relationship between log-fold-change and the statistical significance of differential gene expression.

There is a drastic increase in the number of differentially expressed genes between control and treatment groups in G2 that G1. G4 has the least number of differentially expressed genes between control and treatment groups.

Heatmap of genes that are initially differentially expressed in G1 have an opposite expression pattern in G2. This oscillation continues in G3 and G4, though differential gene expression is dampened.

Euler plot of statistically significant differentially expressed genes between control and treatment groups in each generation shows there is a large amount of unique DEGs compared to the number of overlapping DEGs.

### 10/23/25

Created an RMarkdown file to implement a functional enrichment analysis using `TopGO` with the differential expression contrasts generated from `DESeq2`:

`~/projects/eco_genomics_2025/transcriptomics/mydocs/DESeq2toTopGO.Rmd`

Histogram distributions of DEG counts follow an exponential decline along an axis of log-adjusted p-value, a pattern supported by the combined density-rugplot. 

Copied `Genes_GO_terms_output.tsv`, which maps each gene to GO categories for the species transcriptome to `mydata` for use as input from `TopGO`:

`~/projects/eco_genomics_2025/transcriptomics/mydata/Genes_GO_terms_output.tsv`

Ran `TopGO` with differential gene expression contrasts between G2 samples and revealed enrichment in cellular movement and transport processes.

Created an output of the `TopGO` enrichment results for visualization in `REViGO`:

`~/projects/eco_genomics_2025/transcriptomics/mydata/topGOsig_for_REVIGO.txt`

There was distinct clustering of GO terms from the same parent ontologies on the semantic space axes.

### 10/28/25

Created an RMarkdown file to conduct WGCNA analysis and create a normalized gene expression matrix from DESeq2:

`~/projects/eco_genomics_2025/transcriptomics/mydocs/DESeq2toWGCNA.Rmd`

Imported the trait data file with the upper lethal temperature associated with each sample into the script:

`~/projects/eco_genomics_2025/transcriptomics/mydata/WGCNA_TraitData.csv`

Filtered dataset based on normalized gene expression variance within the samples of a gene to achieve a subset of 7283 genes.

Visualize scale-free topology model fits to choose an appropriate soft-thresholding power. A values between 18 and 25 appear to provide a strong signed correlation for the scale-free topology index and optimizes mean connectivity.

Convert matrix values to numeric and perform the network construction with a soft-thresholding power of 20. Resultant clustering denodogram showed the degree of correlation between modules in the network.

Assessed correlation between module eigengenes and the upper lethal temperature trait data. Modules labeled as MEcyan and MEgrey60 were significantly correlated with the trait data.

Plotted the eigengene values by treatment and line conditions and found that the eigenvalues for both the grey60 and cyan modules differed in G1 and G2, flipping expression between the two generations.

Gene ontology functional enrichment and visualization in REVIGO revealed there was some association with transcriptional/translational regulation as well as with phosphate-containing protein metabolic processes.

### Homework 2

Created an RMarkdown file to prepare run DESeq2, prepare contrasts, and generate TopGO results:

`~/projects/eco_genomics_2025/transcriptomics/mydocs/Homework_2_Results.Rmd`

Used scripts from class activities to run DESeq2, prepare contrasts, and create a results summary of DEGs.

Mean and median logFC was calculated in the significantly up-regulated and down-regulated genes to summarize the magnitude of differential gene expression and compare the distributions of DEGs between contrasts.

While volcano and TopGO plots were structured to resemble those ran in class, generative AI was used to help create functions to loop through each contrast.

To visualize directionality in the functional gene enrichment, up-regulated and down-regulated genes were first subset in each contrast.

Volcano and TopGO plots as well as REVIGO-ready files were saved to a new output folder:

`~/projects/eco_genomics_2025/transcriptomics/mydata/Homework_2_Plots/`