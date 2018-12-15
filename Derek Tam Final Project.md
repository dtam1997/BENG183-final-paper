# ChIP Sequencing (Chromatin Immunoprecipitation Sequencing) 
## Derek Tam
1. [Introduction] <br>
    1.1 [What are Transcription Factors?] <br>
2. [Workflow of ChIP-Seq]
3. [Data Analysis] <br>
    3.1. [A Note on Noise] <br>
    3.2. [Data Visualization] <br>
    3.3. [Encode Project] <br>

## Introduction<a name="231"></a>
ChIP-seq is a powerful technique to explore the physical binding interactions between protein and DNA. ChIP-sequencing combines chromatin immunoprecipitation (ChIP) together with next generation sequencing (Illumina) to create a new high throughput method to screen for all protein-DNA interactions in a sample. ChIP identifies protein-binding sites on chromatin. Chromatin refers to the stretches of DNA wrapped around histone proteins into nucleosomes. The primary-order chromatin refers sections of the chromatin which are unraveled thus exposing DNA for binding. The ability of the cell to dynamically change its gene expression level by modifying its chromatin to be opened or closed is known as epigenetics. It is here where ChIP sequencing can resolve the location and purpose of genomics features on the non-coding regions of DNA such as:
- DNA methylation/acetylation  (Epigenetics)
- Enhancers regions
- Silencers regions
- Insulator regions
- Transcription Factors 

Besides ChIP-seq, there are many other forms of ChIP applications.
- ChIP-Chip: couples chromatin immunoprecipitation to a  microarray which allows for a genome-wide analysis of a protein or modification site of interest.
- ChIP-Seq: uses the same chromatin immunoprecipitation procedure but couples it with next-generation sequencing technology to detect all proteins interacting with DNA. 
- ChIP-exo: specifically developed to map the location of protein of interest (POI) binding sites in the genome. 
- ChIA-PET (Chromatin Interaction Analysis by Paired-End Tag Sequencing) uses chromatin conformation capture (3C) with ChIP technology to detect when distant DNA regions interact with each other through a protein of interest. This provides data on targeted binding factors such as: estrogen receptor alpha, CTCF-mediated loops, RNA polymerase II, and a combination of key architectural factors.[1]

#### What are Transciption Factors?
A key genomic feature ChIP-seq can reveal is the location and expression level of transciption factors bounds to the DNA. Transcription factors are proteins that help activate or inactivate the transcription specific genes by binding to nearby DNA. Activators boost a gene's transcription while repressors decrease transcription. An enhancer sequence is a groups of transcription factor binding sites while silencers have the capability of turning on or off a gene within a specific tissue. Transciption factors are sequence specific. Each one regulates a specific set genes. By analyzing whether or not a sequence is bound by transcription factors, we gain crucial information about the expression of a gene. Transciption factor binding information is very important for the discovery or cure of certain genetic diseases. Detection of these transcription factor binding sites promotes the gene annotation of that sequence. 

## Workflow ChIP-seq<a name="232"></a>
ChIP makes use of reversible cross-links made between DNA and associated proteins by formaldehyde fixation of cells or tissue. The fixed chromatin is physically sheared and DNA fragments associated with a particular protein are selectively immunoprecipitated and analysed. Therefore only the segments of DNA bound by proteins remain. NGS technology makes a read profile of the remaining DNA segments. These reads are mapped to the genome to identify peaks/hotspots where these proteins interactions lie.   

![Process](https://vignette.wikia.nocookie.net/mmg-233-2013-genetics-genomics/images/c/cd/ChIP_Overview.png/revision/latest?cb=20131007202455 "Process")

Figure demonstration library preparation overview.[8]
1. Crosslinking DNA-binding proteins to DNA by treatment of cells with formaldehyde.

2. Preparation of chromatin by sonification or enzymatic digestion.

3. Immunoprecipitation of the crosslinked chromatin is performed using an antibody that recognizes a specific transcription factor or histone isoform.

4. Crosslinks are reversed by heat and proteinase K.

5. Purification of the precipitated fragments, the sample can be analyzed by PCR/Illumina to create the read library.

This creates our library of reads. But now what?

## Data Analysis<a name="232"></a>
The results of the ChIP process produces data of reads representing the sequences of the DNA where proteins where bound. 

But how do we interpret these reads?

![Read alignment](http://i.imgur.com/Ld3Gru6.jpg "Reads")
Figure demonstrating steps of read analysis.[2]

1. Reference genome is chosen. Reads mapped back to reference. (bowtie[2])
    - if necessary, reads can be trimmed out by quality to improve mapping (fastq) 
2. Background noise subtracted by comparing to a reference ChIP sample. 
3. Peak calling determination (MACS2[3])
4. Peaks loaded into visual reader (UCSC Genome/IGV[6])
5. De Novo Motif finding analysis (MEME-ChIP[4]) <br>
    -furthermore a functional analysis of the genes using (GO/DAVID[5]) can be employed

Peak Finding is the most analytical process of ChIP-seq where multiple methods utilized to find true “peaks” in the data. A peak is a site where multiple reads have mapped and produced a pileup. ChIP sequencing is most often performed with single-end reads, and ChIP fragments are sequenced from their 5’ ends only.[8] This creates two distinct peaks; one on each strand with the binding site falling in the middle of these peaks, the distance from the middle of the peaks to the binding site is often referred to as the “shift”.

#### A Note on Noise 
ChIP-seq is designed to generate sequence from specific regions bound to the antibody. However, there are possibilities of background binding/non-specific binding of the antibody which creates non-specific reads known as noise.[9] Noise skews the accuracy of the data. Consequently, ChiP-seq libraries need to be sufficiently large, so the correct reads drown out noise signal. Peak calling therefore is a signal to noise problem. Different applications of algorithms and chosen parameters to determine the interpretation of the data. Steps can be taken such that mapped reads must be restricted to those that map to unique known genome regions only (high specificity), or reads mapping to multiple sites in the genome (high sensitivity).[9] Another step is to increase the size of the fragments making antibodies harder to bind to them. This specificity eliminates random binding. 

#### Data Visualization
Once the peaks have been determined, all the data is compressed into a track or Bedgraph file. This track can be visualized using programs such as IGV or UCSC genome browser to compare the peaks/expression levels between multiple samples.[6] These browsers make it easy to compare by genome species, chromosome number, and nucleotide base location.

![IGV](https://i.ytimg.com/vi/P9n0tZxiwPs/maxresdefault.jpg)
Figure demonstrating use of IGV to compare different ChIP samples. Notice location and intensity of varying peaks.[6]

#### Encode Project
Dozens of labs did ChIP-seq, under rigorous quality guidelines, for over 100 transcription factors and histone modifications, plus related assays for DNA methylation, chromatin accessibility etc.[7] Sequences compiled into public access repository called ENCODE so other researchers can use data for their research. Contains only human and some mouse sequences. modENCODE database eventually created for containing fruit fly and worm sequencing data.

FactorBook: Database compiled from Encode focused on transcription factors, binding motifs, TF-TF interactions, and chromatin features.		
# References
[1] https://github.com/Zhong-Lab-UCSD/BENG183/blob/master/template.md <br>
[2] Langmead, Ben, and Steven L. Salzberg. "Fast gapped-read alignment with Bowtie 2." Nature methods 9.4 (2012): 357. <br>
[3] Zhang, Yong, et al. "Model-based analysis of ChIP-Seq (MACS)." Genome biology 9.9 (2008): R137. <br>
[3] Wilbanks, Elizabeth G., and Marc T. Facciotti. "Evaluation of algorithm performance in ChIP-seq peak detection." PloS one 5.7 (2010): e11471. <br>
[4] Unsupervised Learning of Multiple Motifs in Biopolymers Using Expectation Maximization T.L.Bailey & C.Elkan, C. Machine Learning Journal: 21, 51-83.(1995) <br>
[5] Dennis, Glynn, et al. "DAVID: database for annotation, visualization, and integrated discovery." Genome biology 4.9 (2003). <br>
[6] James T. Robinson, Helga Thorvaldsdóttir, Wendy Winckler, Mitchell Guttman, Eric S. Lander, Gad Getz, Jill P. Mesirov. Integrative Genomics Viewer. Nature Biotechnology 29, 24–26 (2011) <br>
[7] Encode Project Consortium. An integrated encyclopedia of DNA elements in the human genome. Nature. 2012 Sep 6;489(7414):57-74. doi: 10.1038/nature11247. <br>
[8] Figure by Furey, Terrence S. "ChIP–seq and beyond: new and improved methodologies to detect and characterize protein–DNA interactions." Nature Reviews Genetics 13.12 (2012): 840. <br>
[9] Xu, Han, et al. "A signal–noise model for significance analysis of ChIP-seq with negative control." Bioinformatics 26.9 (2010): 1199-1204. <br>


