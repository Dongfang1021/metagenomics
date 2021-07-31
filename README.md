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
### Introduction of Taxonomic Annotation
Taxonomic diversity serves as a way of profiling a community and can be used to ascertain the similarity of two or more communities. This part involves identifying those reads that are marker gene homologs to a database of taxonomically informative gene families, using sequence or phylogenetic similarity to the database sequences (NR database) to taxonomically annotate each metagenomic homolog (MEGAN). According to the abundance table of each taxonomic level, various analyses are performed including Krona analysis, bar plot for abundant species, heatmap of abundance, PCA, NMDs, and differential analysis (Anosim, Metastat and LEfSe analysis).
### Krona presentation
Krona allows hierarchical data to be explored with zoomable pie charts, and aims to answer questions regarding the relative abundance of taxa across multiple levels of the hierarchy simultaneously. The software supplements existing metagenomic visualizations by creating clearer depictions of abundance estimates and by enabling in-depth understanding of the underlying classifications. Please click here for the taxonomic annotation in detail. An example picutre was as follows.
Based on the abundance table of each taxonomic level, the top 10 taxa were picked out and the other taxa were set as "Others". Bar charts show the relative taxonomy abundance of each sample in different taxonomic level.
### PCA and NMDS in taxonomy
Principal Component Analysis (PCA) and Non-Metric Multi-Dimensional Scaling analysis (NMDS) are two main methods used for the dimension reduction analysis. PCA uses an orthogonal transformation to convert a sset of possibly correlated variables into a set of values of linearly uncorrelated variables called principal components. The PCA transformation ensures that the horizontal axis PC1 accounts for the most variation, the vertical axis PC2 the second-most. For the community composition of samples, more similar they are, closer sample points in the PCA figure could show. And NMDS is a ranking method applicable to ecological researchers. It is a non-linear model designed for a better representation of non-linear biological data structure.
### PCoA in taxonomy
Principal coordinates analysis (PCoA) is an ordination technique, which picks up the main elements and structure from reduced multi-dimensional data series of eigenvalues and eigenvectors. The technique has the advantage over PCA that each ecological distance can be investigated. Gathered samples represent high species composition similarity than the separate ones. PCoA result based on Bray-Curtis distance was shown as follows.
### Anosim analysis
Anosim is a nonparameteric test to evaluate whether variation among groups is significiantly greater than variantion within groups, which helps to evaluate the reasonability of the divisioln of groups. 
### Sample clustering with taxonomic abundance
Sample clustering analysis based on Bray-Curtis distance can evaluate the similarity of samples. The distance was calculated according to relative taxonomic abundance. And the final results were exhibited by combining the clustering result and relative abundance of different samples in phylum level.
### LEfSe analysis
LEfSe (linear discriminant analysis (LDA) Effect Size) analysis allows high-dimensional biomarker discovery and explanation. LEfSe identifies genomic features (genes, pathways or taxa) characterizing the differences between two or more biological conditions (or classes). It enables the characterization of microbial taxa specific to an experimental or environmental condition, and the identification of metagenomic biomarkers in different communities.
Based on the species abundance differences among the groups screened by the above-mentioned LEfSe, the biomarkers at a particular taxonomic level (default genus) were selected to draw the cluster heatmap to reflect the distribution of the biomarkers in each sample. 

## Function Annotation
### Introduction of function annotation
Metagenomes provide insight into the physiology of a community by clarifying the collective functions that are encoded in the genomes of the organisms that make up the community. The functional diversity of a community can be quanitified by annotating metagenomic sequences with functions (one HSP > 60 bits). Classification of an assembled metagenomic protein sequence into protein family (function) usually requires comparing the metagenomic protein to either a database of protein sequences, each of which is designated as a memger of a family. Protein coding sequences were mapped against functional database listed as the following sources:
- Kyoto Encyclopedia of Genes and Genomes (KEGG).
  KEGG is an integrated database resource consisting of eighteen databases (including computationally generated SSDB), in which KEGG PATHWAY and KEGG ORTHOLOGY (KO) are the core database is a database of molecular functions represented in terms of functional orthologs. KEGG PATHWAY is a reference database for Pathway Mapping and each Mapping and each pathway can be divided into three levels. Besides, KEGG ENZYME (ec) is also used in function annotation.
- Evolutionary genealogy of genes: Non-supervised Orthologues Groups (eggNOG), Version 4.1
  Eggnog, the database of orthologous groups and functional annotation, can be divided into 24 categories in the first level, and each category is represented by a capital letter.
- Carbohydrate-Active enzymes Database(CAZy), Version:2014.11.25
  CAZy is a database dedicated to the display and analysis of genomic, structural and biochemical information on Carbohydrate-Active Enzymes. The database mainly contains six functional classes in the first level: Glycoside Hydrolase, GlycosylTransferase, Polysaccharide Lyase, Carbohydrate Esterases, Auxiliary Activivities and Carbohydrate-Binding Modules
A range of multivariate statistical analyses were the comparison of relative functional abundance against KEGG, eggNOG and CAZy on multiple levels of resolution. More details in the three databases involved in function annotation were showed as follows:
According to the functional abundance, various analyses were performed including bar chart, clustering heatmap, PCA, NMDS analysis, Anosim, Metastats, LEfSe analysis and pathway analysis.
### Functional abundance
Based on Unique genes annotation results, cartogram of annotated gene number of each database was drawn. The results were showed as follows.
### Relative abundance of function
According to the relative abundance in level 1 of each database, cartogram of the functional abundance of each sample was drawn.
### Function distribution heatmap
Function clustering selects the dominant 35 functions based on the abundance table in each database. The abundance distribution of these dominant 35 functions was displayed by heatmap.
### PCA and NMDS in function
PCA and NMDS based on functional abundance in level 2 of each database were shown as follows.
### PCoA in function
PCoA based on Bray-Curtis distance in level 1 of each database were shown as follows.
### Sample clustering with functional abundance
In order to study the similarity of different samples, clustering analysis was conducted based on Bray-Curtis distance which is usually used to indicate the similarity between samples.
### Metabolic pathway
To study the variances of pathway patterns in different groups (samples), the web version pathway report was created. The whole pathway report has two parts:
Part1 (mPath): mPath is statistical package for comparing metagenomic data-sets in the pathway level (using KEGG pathway information). Metapath relies on a graph-theoretic definition of statistical significance in order to identify pathway motifs that differ between groups or samples from two treatment populations. In this part, the compared pathway overview shows shared and unique pathway information between groups or samples. Nodes represent chemicals, and lines represent enzymatic reactions, of which the shared ones are marked in red, while the unique ones are marked in blue(group A/sample A) or grean (group B/sample B)
Part2 The annotated metabolic pathway. In this part, nodes represent chemicals. Rectangle represent enzymes and different colors represent different Unigene numbers (the numbers increase from blue to red); Touching your mouse on the colored rectangles, the Genes ID annoated will be displayed. Rectangles filled in yellow are those significantly variant among groups (if there is no such analysis, the information will not display); Touching your mouse on the enzymes, the box chart for enzymes with significantly variant abundance will be displayed.
### Metastatis analysis of functional differences
Functions whose abundance were signficantly different were detected via Metastats, a statistical methods for detecting differentially abundant features.
Significantly different function heatmap and PCA
### LEfSe analysis of functional differences
LEfSe (linear discriminant analysis (LDA) Effect Size) analysis allows high-dimensional biomarker discovery and explannation. LEfSe identifis genomic features (genes, pathways or taxa) characterizing the differences between two or more biological conditions (or classes). It enables the characterization of microbial taxa specific to an experimental or environmental condition, and the identification of metagenomic biomarkers in different communities. In order to detect biomarkers with statistical diferences among groups, function with significant differences was detected via Kruska-Wallis test, and then LDA score was calculated. The LDA distribution of differential function was shown as follows.
Heatmap analysis was performed to study the distribution of biomarkers.
Based on taxonomic abundance table and function abundance table, clustering analysis, Anosim, PCA and NMDS could be carried out. When grouping information was available, Metastats and LEfSe multivariate statistical analysis and comparative analysis of metabolic pathways could be carried out to explore species composition and functional composition differences between groups.
## Antibiotic Resistant Gene (ARGs) Analysis
Against Antibiotic Resistance gene Database(CARD, ARDB) for annotation, ARGs abundance and distribution in species classification could be obtained.
Efforts on identifying new antibiotics were once a top research and development priority among pharmaceutical companies. However, the treatment of infections is increasingly compromised by the ability of bacteria to develop resistance to antibiotics through mutation or acquisition of resistance genes. Antibiotic resistance genes are also potentially used by bio-terrorists in genetically modified organisms. CARD(the Comprehensive Antibiotic Research Database) database is used to facilitate identification and characteriztion of antibiotic resistance genes. Resistance genes are further categorized to resistance types by their resistance profiles and sequence similaryti. Each gene or type is annotated with rich information, including resistance profile and resistance mechanism.
### Introduction of antibiotic resistance gene annotation
- All unique genes were blastp against CARD database (blastp, evalue<=1e-5)
- Relative abundance of different resistance genes were calculated based on above results.
- According to the abundance table of resistance genes, various analyses were performed.
### Relative abundance of resistance genes
To make it more convenient for the observation of the overall proportion and distribution of the resistance genes in the sample, overview circle  chart was drawn and shown as follows.
### Distribution of antibiotic resistance genes
In order to reflect the distribution of antibiotic resistance genotype (ARG) in each sample, black and white graph of the ARG distribution was drawn. At the same time, according to the abundance information of ARG in each sample, the 30 ARGs were selected to draw the abundance clustering heatmap. The results were shown as follows.
Note
1) When the number of samples is less than 3, PCA, NMDS, CCA/RDA,clustering analysis and abundance heatmap analysis cannot be carried out.
2) When the number of biological repeats in the group is less than 3, statistical analysis such as Anosim, Metastat, and LEfSe are statistically meaningless and the analysis cannot be conducted.

