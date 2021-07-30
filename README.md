# Metagenomics workflow
## Data Quality Control
The protocols of data pre-processing are as follows:
1) Trim low quality bases (Q-value <= 38) which exceed certain threshold (40 bp by default)
2) Trim reads which contain N nucleotides over certain threshold (10 bp by default)
3) Trim reads which overlap with adatper over certain threshold(15 bp by default)
4) If the target community is associated with a host, soap2.21 was used to minimalize host DNA.
## Metagenome Assemblyed
1) Samples passing QC were assembled initially using an optimized SOAPdenovo protocol for Gut, or MEGAHIT for soil and Water (K-mer=55)
2) The scaffolds were cut off at "N" to get fragments without "N", called Scaftigs(i.e., coninuous sequences within scaffolds)
3) Clean data of all samples were mapped to assembled Scaftigs using Soap 2.21 and unutilized PE reads were collect.
4) Mixed assembly was conducted on the unutlized reads with the same assemble parameter.
5) The scaftigs of each sample and mixed assembled, which were less than 500 bp, were trimmed. And the effective Scaftigs were used of further analysis and gene prediction.
## Gene Predication
### Introduction of gene prediction and abundance analysis
1) Scaftigs (>=500bp) were used for ORF (Open Reading Frame) predication by MetaGeneMark. The ORFs less than 100nt were trimmed.
2) The ORFs were dereplicated by CD-HIT to generate gene catalogues (Herein, the non-redundant continuous gene encoding the nucleic acid sequence is called genes). Dereplicating by default: identity = 95%, coverage = 90%. The longest one was chose as representive gene (unigene). CD-HIT parameter: -c 0.95, -G 0, -aS 0.9, -g 1, -d 0
3) Clean data were mapped to gene catalogue using SoapAligner to calculate the quantity. Paramenter: -m 200, -x 400, identity >= 95%
4) The gene abundance was calculated based on the total number of mapped reads and gene length. Computational formula was as follows:
5) Downstream analyses were performed based on the abundance of gene catalogues.
### Gene catalogue statistics
### Core-pan genome analysis
Based on the gene abundance table, rarefaction curves were plotted with the number of core-genes and pan-genes separtely by randomly drawing sampling, the figures were shown as follows:
### Gene number analysis
To investigate the difference of gene number among groups, the gene number of different groups was shown as follows in box chart.
To investigate the number of the common and peculiar genes among specified samples (groups), Venn figures were drawn as follows.
### Correlation analysis of samples
The correlation coefficient between samples is a critical index which reflects the reliability of experiment and the reasonability of the chosen samples. 
## Taxonomy Annotation
## Function Annotation
## Based on taxonomic abundance table and function abundance table, clustering analysis, Anosim, PCA and NMDS could be carried out. When grouping information was available, Metastats and LEfSe multivariate statistical analysis and comparative analysis of metabolic pathways could be carried out to explore species composition and functional composition differences between groups.
## Antibiotic Resistant Gene (ARGs) Analysis: Against Antibiotic Resistance gene Database(CARD, ARDB) for annotation, ARGs abundance and distribution in species classification could be obtained.
Note
1) When the number of samples is less than 3, PCA, NMDS, CCA/RDA,clustering analysis and abundance heatmap analysis cannot be carried out.
2) When the number of biological repeats in the group is less than 3, statistical analysis such as Anosim, Metastat, and LEfSe are statistically meaningless and the analysis cannot be conducted.

