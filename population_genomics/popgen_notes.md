# Population Genomics Notebook

## Fall 2025 Ecological Genomics

## Author: Aidan Jones

This will keep my notes on population genomics coding sessions

### 09/11/25: Cleaning fastq reads of red spruce

We wrote a bash script called "fastp.sh" located within my GitHub repo:

`~/projects/eco_genomics_2025/population_genomics/myscripts`

We used this to trim the adapters out of our red spruce fastq sequence files.

The raw fastq files were located onthe class shared space:

`/gpfs1/cl/ecogen/pbio6800/PopulationGenomics/fastq/red_spruce`

Using the program fastp, we processed the raw reads and output the cleaned reads to the following directory on the class shared space:

`/gpfs1/cl/ecogen/pbio6800/PopulationGenomics/cleanreads`

Fastp produced html-formatted reports for each sample, which I saved into the directory:

`~/projects/eco_genomics_2025/population_genomics/myresults/fastp_reports`

The results showed high quality sequence, with most Q-scores being much greater than 2, and low amount of adapter contamination, which we trimmed out. We also trimmed out the leading 12 bp to get rid of the barcoded indices.

Cleaned reads are now ready to proceed to the next step in our pipeline which is mapping the reads to the reference genome.

### 09/16/25: Mapping our cleaned reads to the reference genome

We are using the sister species black spruce (Picea mariana) reference genome to map our red spruce sequecing reads to.

Reference genome was blasted against our 80,000 exome capture probes to exclude repetitive non-protein coding regions.

The indexed reduced genome used for mapping is in the class shared space:

`/gpfs1/cl/ecogen/pbio6800/PopulationGenomics/ref_genome/Pmariana/Pmariana-genome_reduced.fa`

Mapping was performed using the `bwa-mem2` program in the custom script:

`~/projects/eco_genomics_2025/population_genomics/myscripts/mapping.sh`

Processing the the sequence alignment files (.sam) was performed using the `sambamba` program in the custom script:

`~/projects/eco_genomics_2025/population_genomics/myscripts/process_bam.sh`

This script converted the sam alignment files to a bam format with `view`, sorted the bam files by its read coordinates with `sort`, marked and removed any PCR duplicate reads with `markdup`, and indexed the processed alignment file with `index`.

Mapping statistics were calculated using the `samtools` program in the custom script:

`~/projects/eco_genomics_2025/population_genomics/myscripts/bam_stats.sh`

Basic information about sequence mapping was gather with `flagstat` and depth of coverage was estimated with `depth`.

A simple wrapper bash script was created to run these scripts in a single pipeline:

`~/projects/eco_genomics_2025/population_genomics/myscripts/process_stats_wrapper.sh`

