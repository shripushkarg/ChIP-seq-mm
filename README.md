# ChIP-seq

## Methods

FastQC v0.11.9 will be used to assess the quality of raw sequencing reads. Quality metrics, including sequence quality, GC content, length distribution, and possible contamination, are to be analyzed. Trimming of sequencing reads will be performed using Trimmomatic v0.39 on FASTQ files, using the provided adapter file. The following parameters are to be applied: ILLUMINACLIP:{adapters}:2:30:10 LEADING:3 TRAILING:3 SLIDINGWINDOW:4:15. The mouse reference genome (GRCm39) should be indexed using Bowtie2 v2.4.2. FASTQ files will be aligned to the reference genome using Bowtie2, and SAM files will be automatically converted to BAM format using Samtools within the same command. The annotation file is mouse vM34 from gencode.  

Sorted and indexed BAM files will be generated using Samtools v1.12, which provide efficient downstream analysis. Samtools flagstat provide quick quality checks on alignments. BAM files will be converted to bigWig format using Deeptools' bamcoverage utility for downstream analysis and visualization. The default parameters should be used for this conversion. MultiQC should be utilized for compiling QC data. HOMER will be employed for peak calling with the findPeaks command, comparing RUNX1 replicates with INP control samples. The makeTagDir command will be used for each sample prior to peak calling, utilizing default parameters. HOMER-specific output will be converted to BED format using the pos2bed utility.

Reproducible peaks will be identified using Bedtools' intersect command and filtered against hg38 blacklist regions to remove signal-artifact regions. Peaks will be annotated to genomic features using HOMER's annotatePeaks.pl command, with default parameters and provided GTF file.
HOMER's findMotifsGenome.pl command will be used for motif finding in reproducible peaks, to identify enriched motifs. Deeptools' multiBigWigSummary and plotCorrelation utilities will generate heatmaps of Pearson correlation values between samples. Visualizations will be created using bigWig files and the UCSC Table Browser's gene coordinates BED file. Deeptools' computeMatrix and plotProfile utilities provide signal coverage plots across gene bodies, using default parameters for both commands.

## Questions to Address

1. Briefly remark on the quality of the sequencing reads and the alignment statistics, make sure to specifically mention the following:
  - Are there any concerning aspects of the quality control of your sequencing reads?
  - Are there any concerning aspects of the quality control related to alignment?
  - Based on all of your quality control, will you exclude any samples from further analysis?
2. After QC, generate a “fingerprint” plot (see deeptools utility) and a heatmap plot of correlation values between samples.
  - Briefly remark on the plots and what they indicates to you in terms of the experiment.
3. After performing peak calling analysis, generating a set of reproducible peaks and filtering peaks from blacklisted regions, answer the following:
  - How many peaks are present in each of the replicates?
  - How many peaks are present in your set of reproducible peaks? What strategy did you use to determine “reproducible” peaks?
  - How many peaks remain after filtering out peaks overlapping blacklisted regions?
4. After performing motif analysis and gene enrichment on the peak annotations, answer the following:
  - Briefly discuss the main results of both of these analyses and what they might imply about the function of the factor we are interested in.

## Deliverables

1. Produce a heatmap of correlation values between samples.
2. Generate a “fingerprint” plot using the deeptools plotFingerprint utility.
3. Create a figure / table containing the number of peaks called in each replicate, and the number of reproducible peaks.
4. A single BED file containing the reproducible peaks you determined from the experiment.
5. Perform motif finding on your reproducible peaks.
  - Create a single table / figure with the most interesting results.
6. Perform a gene enrichment analysis on the annotated peaks using a well-validated gene enrichment tool.
  - Create a single table / figure with the most interesting results.
7. Produce a figure that displays the proportions of where the factor of interest is binding (Promoter, Intergenic, Intron, Exon, TTS, etc.)

