# ChIP Sequencing (Chromatin Immunoprecipitation Sequencing) 
1. [Introduction]
    1.1 [What are Transcription Factors?]
2. [Workflow of ChIP-Seq]
3. [Data Analysis]
    3.1. [A Note on Noise]
    3.2. [Data Visualization]
    3.3. [Encode Project]


## Introduction<a name="231"></a>
It is a powerful tool to analyze protein-DNA interactions
Very useful in identifying sequences that are bound by transcription factors, histone modifications, or RNA polymerase in vivo
Used to examine function of non-coding regions such as enhancers, silencers, insulators
It is able to reveal the gene regulation events that play a role in biological pathways and even diseases, such as cancer

ChIP-seq is a powerful technique to explore the physical binding interactions between protein and DNA. ChIP-sequencing combines chromatin immunoprecipitation (ChIP) together with next generation sequencing (Illumina) to create a new high throughput method. Chromatin immunoprecipitation (ChIP) has evolved into multiple methods to identifying protein-binding sites on chromatin. Chromatin refers to the stretches of DNA wrapped around histone proteins into nucleosomes. The primary-order chromatin refers sections of the chromatin which are unraveled thus exposing DNA. The ability of the cell to dynamic change its gene expression level by modifying its chromatin to be opened or closed is known as epigetic modifications. It is here where ChIP sequencing can resolve the protein-DNA interactions on the non-coding region of DNA such as:
- DNA methylation/acetylation  (Epigenetics)
- Enhancers regions
- Silencers regions
- Insulator regions 
- Transcription Factors 

The first ChIP technologies was Chip-chip which eventually developed into other forms of ChIP.
- ChIP-Chip: couples chromatin immunoprecipitation to a  microarray which allows for a genome-wide analysis of a protein or modification sites of interest.
- ChIP-Seq: uses the same chromatin immunoprecipitation procedure but couples it with next-generation sequencing technology to detect all proteins interacting with DNA. 
- ChIP-exo: specifically developed to map protein of interest (POI) binding sites in the genome. 
- ChIA-PET (Chromatin Interaction Analysis by Paired-End Tag Sequencing) uses chromatin conformation capture (3C) with ChIP technology to detect when distant DNA regions interact with each other through a protein of interest. This provides data on targeted binding factors such as: estrogen receptor alpha, CTCF-mediated loops, RNA polymerase II, and a combination of key architectural factors. 

#### What are Transciption Factors?
A crucial data point ChIP sequencing can reveal is the location level of transciption factors bounds to the DNA. Transcription factors are proteins that help activate or inactivate the transcription specific genes by binding to nearby DNA. Transcription factors that are activators boost a gene's transcription while repressors decrease transcription. An enhancer sequence is a groups of transcription factor binding sites while silencers have the capability of turning on or off a gene within specific tissue. Transciption factors are sequence specific. Each one regulates a specific set genes. By analyzing whether or not a sequence is bound to TF, we gain crucial information about the transcription of a gene. Transciption factor binding information is very important in the discovery or curing of certain diseases. Detection of these transcription factor binding sites promotes the gene annotation of that sequence. 

## Workflow ChIP-seq<a name="232"></a>
ChIP makes use of reversible cross-links made between DNA and associated proteins by formaldehyde fixation of cells or tissue. The fixed chromatin is physically sheared and DNA fragments associated with a particular protein are selectively immunoprecipitated and analysed. Therefore only the segments of DNA bound by proteins remain. NGS technology makes a read profile of the remaining DNA segments. These reads are mapped to the genome to identify peaks/hotspots where these proteins interactions lie.   

![Process](https://vignette.wikia.nocookie.net/mmg-233-2013-genetics-genomics/images/c/cd/ChIP_Overview.png/revision/latest?cb=20131007202455 "Process")

Library Preparation
1. Crosslinking DNA-binding proteins to DNA by treatment of cells with formaldehyde

2. Preparation of chromatin by sonication or enzymatic digestion.

3. Immunoprecipitation of the crosslinked chromatin is performed using an antibody that recognizes a specific transcription factor or histone isoform

4. Crosslinks are reversed by heat and proteinase K.

5. Purification of the precipitated fragments, the sample can be analyzed by PCR/Illumina to study particular genes.

This creates our library of reads. But what now?

## Data Analysis<a name="232"></a>
The results of the ChIP process produces data of reads representing the sequences of the DNA where proteins where bound. 

But how do we interpret these reads?

![Read alignment](http://i.imgur.com/Ld3Gru6.jpg "Reads")
1. Reference genome is chosen. Reads mapped back to reference. (bowtie)
    - if necessary, reads can be trimmed out by quality to improve mapping (fastq) 
2. Background noise subtracted by comparing to a reference ChIP sample. 
3. Peak calling determination (MACS2)
4. Peaks loaded into visual reader (UCSC Genome/IGV)
5. De Novo Motif finding analysis (MEME-ChIP)
    -furthermore a functional analysis using (GO/DAVID) can be employed

Peak Finding is the most analytical process of ChIP-seq where multiple methods utilized to find true “peaks” in the data. A peak is a site where multiple reads have mapped and produced a pileup. ChIP sequencing is most often performed with single-end reads, and ChIP fragments are sequenced from their 5’ ends only. This creates two distinct peaks; one on each strand with the binding site falling in the middle of these peaks, the distance from the middle of the peaks to the binding site is often referred to as the “shift”.


#### A Note on Noise 
ChIP-seq is designed to generate sequence from only specific regions bound to the antibody target. However, there are possibilities of backgroudn binding/non-specific binding of the antibody which creates non-specific reads known as noise. Noise skews the accuracy of the data. Consequently, ChiP-seq libraries need to be sufficiently large, so the correct reads drown out noise signal. Peak calling therefore is a signal to noise problem. Different applications of algorithms and chosen parameters to determine the interpretation of the data. Steps can be taken such that mapped reads must be restricted to those that map to unique known genome regions only (high specificity), or reads mapping to multiple sites in the genome (high sensitivity). Another step is to increase the size of the framents making antibodies harder to bind to them. This specificity eliminates random binding. 



#### Data Visualization
Once the peaks have been determined, all the data is compressed into a track. This track can be visualized using programs such as IGV or UCSC genome viewer to compare the peaks/expression levels between multiple samples. These browsers make it compare by genome species,  chromosome number, and nucleotide base location.

![IGV](https://i.ytimg.com/vi/P9n0tZxiwPs/maxresdefault.jpg)
Figure demonstrating use of IGV to compare different ChIP samples. Notice location and intensity of varying peaks.[6]

#### Encode Project
Dozens of labs did ChIP-seq, under rigorous quality guidelines, for over 100 transcription factors and histone modifications, plus related assays for DNA methylation, chromatin accessibility etc.[7] Sequences compiled into public access repository called ENCODE so other researchers can use data for their research. Contains only human and some mouse sequences. modENCODE database eventually created for containing fruit fly and worm sequencing data.

FactorBook: Database compiled from Encode focused on transcription factors, binding motifs, TF-TF interactions, and chromatin features.		


# Referrence
[1] 

[2] 
[3] 
[4] 
[5] 
[6] James T. Robinson, Helga Thorvaldsdóttir, Wendy Winckler, Mitchell Guttman, Eric S. Lander, Gad Getz, Jill P. Mesirov. Integrative Genomics Viewer. Nature Biotechnology 29, 24–26 (2011)
[7] Encode Project Consortium. An integrated encyclopedia of DNA elements in the human genome. Nature. 2012 Sep 6;489(7414):57-74. doi: 10.1038/nature11247.


[8] https://github.com/hms-dbmi/hic-data-analysis-bootcamp/blob/master/HiC-Protocol.pptx.

