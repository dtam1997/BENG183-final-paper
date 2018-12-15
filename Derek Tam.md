# ChIP Sequencing (Chromatin Immunoprecipitation Sequencing) 
1. [Introduction]
2. [Workflow]
    2.1. [Specificity](#2321)<br>
    2.2. [Through-put and resolution](#2322)
3. [Data Analysis]
4. [Application]




## Introduction<a name="231"></a>


It is a powerful tool to analyze protein-DNA interactions
Very useful in identifying sequences that are bound by transcription factors, histone modifications, or RNA polymerase in vivo
Used to examine function of non-coding regions such as enhancers, silencers, insulators
It is able to reveal the gene regulation events that play a role in biological pathways and even diseases, such as cancer


ChIP-seq is a powerful technique to explore the physical binding interactions between protein and DNA. ChIP-sequencing combines chromatin immunoprecipitation (ChIP) together with next generation sequencing (Illumina) to create a new high throughput method. 

Chromatin immunoprecipitation (ChIP) has evolved into multiple methods to identifying protein-binding sites on chromatin. Chromatin refers to the stretches of DNA wrapped around histone proteins into nucleosomes. The primary-order chromatin refers sections of the chromatin which are unraveled thus exposing DNA. It is here where ChIP sequencing can resolved the protein-DNA interactions which encompasses DNA methylation sites, enhancer, silencer, insulator regions, as well as transcription factors. The ability of the cell to dynamic change its gene expression level by modifying its chromatin to be opened or closed is known as epigetic modifications.


The first ChIP technologies was Chip-chip which eventually developed into other forms of ChIP.
-ChIP-Chip: couples chromatin immunoprecipitation to a  microarray which allows for a genome-wide analysis of a protein or modification sites of interest.
-ChIP-Seq: uses the same chromatin immunoprecipitation procedure but couples it with next-generation sequencing technology to detect all proteins interacting with DNA. 
-ChIP-exo: specifically developed to map protein of interest (POI) binding sites in the genome. 
-ChIA-PET (Chromatin Interaction Analysis by Paired-End Tag Sequencing) uses chromatin conformation capture (3C) with ChIP technology to detect when distant DNA regions interact with each other through a protein of interest. 


ChIA-PET is another method that combines ChIP and pair-end sequencing to analysis the chromtin interaction. It allows for targeted binding factors such as: estrogen receptor alpha, CTCF-mediated loops, RNA polymerase II, and a combination of key architectural factors. on the one hand, it has the benefit of achieving a higher resolution compared to Hi-C, as only ligation products involving the immunoprecipitated molecule are sequenced, on the other hand, ChIA-PET has systematic biases due to ChIP process:
- Only one type of binding factor selected
- Different antibodies
- ChIP conditions


#### What are Transciption Factors?
A crucial data point ChIP sequencing can reveal is the location level of transciption factors bounds to the DNA. Transcription factors are proteins that help activate or inactivate the transcription specific genes by binding to nearby DNA. Transcription factors that are activators boost a gene's transcription while repressors decrease transcription. An enhancer sequence is a groups of transcription factor binding sites while silencers have the capability of turning on or off a gene within specific tissue. Transciption factors are sequence specific. Each one regulates a specific set genes. By analyzing whether or not a sequence is bound to TF, we gain crucial information about the transcription of a gene. Transciption factor binding information is very important in the discovery or curing of certain diseases. Detection of these transcription factor binding sites promotes the gene annotation of that sequence. 






## Overivew of ChIP method<a name="232"></a>

ChIP makes use of reversible cross-links made between DNA and associated proteins by formaldehyde fixation of cells or tissue. The fixed chromatin is physically sheared and DNA fragments associated with a particular protein are selectively immunoprecipitated and analysed. 

![Process](https://vignette.wikia.nocookie.net/mmg-233-2013-genetics-genomics/images/c/cd/ChIP_Overview.png/revision/latest?cb=20131007202455 "Process")

Library Preparation
1. Crosslinking DNA-binding proteins to DNA by treatment of cells with formaldehyde

2. Preparation of chromatin by sonication or enzymatic digestion.

3. Immunoprecipitation of the crosslinked chromatin is performed using an antibody that recognizes a specific transcription factor or histone isoform

4. Yield the collection of all the binding sites in the genome for the factor of interest.

5. Purification of the precipitated fragments, the sample can be analyzed by PCR/Illumina to study particular genes.





## Data Analysis<a name="232"></a>
The results of the ChIP process produces data of reads representing the sequences of the DNA where proteins where bound. 

But how do we interpret these reads?
![Read alignment](http://i.imgur.com/Ld3Gru6.jpg "Reads")
1. Reference genome is chosen. Reads mapped back to reference. (bowtie)
    - if necessary, reads can be trimmed out by quality to improve mapping (fastq) 
2. Background noise subtracted
3. Peak calling determination (MACS2)
4. Peaks loaded into visual reader (UCSC Genome/IGV)
5. De Novo Motif finding analysis (MEME-ChIP)
    -furthermore a functional analysis using (GO/DAVID) can be employed


Peak calling using MACS2
Motif finding
 Function analysis for up/down regulated gene
Data visualization (Part 3)   

Peak calling (MACS2)
Sequencing depth normalization
Adjust p-value and fdr
True positive peak compared to input data 
Compare peak position with CpG islands and TSS for further validation*

Motif finding (MEME-ChIP)

Functional analysis (GO / DAVID)
up/down regulated genes
across sample comparison


#### Encode Project
Dozens of labs did ChIP-seq, under rigorous quality guidelines, for over 100 transcription factors and histone modifications, plus related assays for DNA methylation, chromatin accessibility etc. Contains only human and some mouse sequences. modENCODE database eventually created for containing fruit fly and worm sequencing data.

Encode Project Consortium. An integrated encyclopedia of DNA elements in the human genome. Nature. 2012 Sep 6;489(7414):57-74. doi: 10.1038/nature11247.

FactorBook: Database compiled from Encode focused on transcription factors, binding motifs, TF-TF interactions, and chromatin features.		



#### 1) Specificity - What does _one, all, many_ mean<a name="2321"></a>
‘1’, ‘Many’ and ‘All’ indicate how many loci are interrogated in a given experiment. For example, ‘1 versus All’ indicates that the experiment probes the interaction profile between 1 locus and all other potential loci in the genome. ‘All versus All’ means that one can detect the interaction profiles of all loci, genome-wide, and their interactions with all other genomic loci [1].

These kind of specificity is determined by the primer when people use **specific primers** before PCR. 

#### 2) Through-put and resolution<a name="2322"></a>
Hi-C techniques has the highest through-put (billion reads per sample) but suffering of a relative low resolution of 0.1-1Mb. However, the other methods usually have a higher resolution  around 1kb. For more details one can refer to table2 in [2].

## 2.3.3 Hi-C<a name="233"></a>
Hi-C is the highest through-put version of 3C-derived technologies. Due to the decreasing cost of 2nd generation sequencing, hi-c is widely used.

The principle of Hi-C can be illustrated as:
![](/assets/hic.gif)


##### Hi-C critical steps [8] 
- Fixation: keep DNA conformed
- Digestion: enzyme frequency and penetratin
- Fill-in: biotin for junction enrichment
- Ligation: freeze interactions in sequence
- Biotin removal: junctions only
- Fragment size: small fragments sequence better
- Adapter ligation: paired-end and indexing
- PCR: create enough material for flow cell




## 2.3.5 Selected methods comparison<a name="235"></a> 
<table>
 <tbody>
    <tr>
        <th>Method</td>
        <th>Targets</td>
        <th>Resolution</td>
        <th>Notes</td>
    </tr>
    <tr>
        <td>3C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0535">[3]</a></td>
        <td>one-vs-one</td>
        <td>~1–10 kb<br></td>
        <td><ul><li>Sequence of bait locus must be known</li><li>Easy data analysis</li><li>Low throughput</li></ul></td>
    </tr>
    <tr>
    <td>4C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0545">[4]</a></td>
    <td>one-vs-all</td>
    <td>~2 kb</td>
    <td><ul><li>Sequence of bait locus must be known</li><li>Detects novel contacts</li><li>Long-range contacts</li></ul></td>
    </tr>
    <tr>
    <td>5C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0550">[5]</a></td>
    <td>many-vs-many</td>
    <td>~1 kb</td>
    <td><ul><li>High dynamic range</li><li>Complete contact map of a locus</li><li>3C with ligation-mediated amplification (LMA) of a ‘carbon copy’ library of oligos designed across restriction fragment junctions of interest
3C</li></ul></td>
    </tr>
    <tr>
    <td>Hi-C <a href="http://refhub.elsevier.com/S2001-0370(17)30093-4/rf0300">[6]</a></td>
    <td>all-vs-all</td>
    <td>0.1–1 Mb</td>
    <td><ul><li>Genome-wide nucleosome core positioning</li><li>Relative low resolution</li><li>High cost</li></ul></td>
    </tr>
    <tr>
    <td>ChIA-PET <a href="http://refhub.elsevier.com/S0168-9525(15)00063-3/sbref1405">[7]</a></td>
    <td>Interaction of whole genome mediated by protein</td>
    <td>Depends on read depth and the size of the genome region bound by the protein of interest</td>
    <td><ul><li>Lower noise with ChIP</li><li>Biased method since selected protein</li></ul></td>
    </tr>
 </tbody>
</table>

















# Referrence
[1] Schmitt, Anthony D., Ming Hu, and Bing Ren. "Genome-wide mapping and analysis of chromosome architecture." Nature reviews Molecular cell biology 17.12 (2016): 743.<br>

[2] Risca, Viviana I., and William J. Greenleaf. "Unraveling the 3D genome: genomics tools for multiscale exploration." Trends in Genetics 31.7 (2015): 357-372.<br>

[3] Dekker J, Rippe K, Dekker M, Kleckner N. Capturing chromosome conformation. Science 2002;295(5558):1306–11.<br>

[4] Simonis M, Klous P, Homminga I, Galjaard RJ, Rijkers EJ, Grosveld F, et al. High-res- olution identification of balanced and complex chromosomal rearrangements by 4C technology. Nature Methods 2009;6(11):837–42.<br>

[5] Dostie J, Richmond TA, Arnaout RA, Selzer RR, Lee WL, Honan TA, et al. Chromo- some Conformation Capture Carbon Copy (5C): a massively parallel solution for mapping interactions between genomic elements. Genome Res 2006;16(10): 1299–309.<br>

[6] Lieberman-Aiden E, van Berkum NL, Williams L, Imakaev M, Ragoczy T, Telling A, et al. Comprehensive mapping of long-range interactions reveals folding principles of the human genome. Science 2009;326(5950):289–93.<br>

[7] Fullwood, M.J. et al. (2009) An oestrogen-receptor-alpha-bound human chromatin interactome. Nature 462, 58–64.<br>

[8] https://github.com/hms-dbmi/hic-data-analysis-bootcamp/blob/master/HiC-Protocol.pptx.

