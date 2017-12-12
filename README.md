Introduction to Differential Expression Analysis using edgeR and DESeq2 packages in R

Biology

In organisms, genes may be expressed at different rates under different conditions – that is, producing different numbers of mRNA for the same gene. For instance, an organism under heat stress may have a proportion of its cells expressing heat-shock proteins, whereas at normal temperatures these genes might be lowly expressed. Cancer cells in vitro may express more protective genes under chemotherapy stress. In the case of individuals with different phenotypes, there may be differences in constitutive gene expression levels. In contrast, so-called maintenance genes are expected to have little differential expression, even under different conditions.  (Only a small proportion of genes will be significantly differentially expressed between two experimental conditions.)

Experiments

The purpose of differential expression analysis is to quantify the difference in counts of some type of genetic material – usually mRNA – between two organisms or populations experiencing different environmental conditions, or exhibiting a difference in phenotype.

For RNA-seq, next generation sequencing (NGS) methods are harnessed for quantifying mRNA. RNA is pulled down from the cellular samples, amplified (copied many times to increase the reads per gene), and then sequenced. The number of reads of sequences from the same DNA span is the relative quantity of an mRNA at the time of sampling, 

Cautions

It is important to note that sequencing and quantification of mRNA is only that: measuring the quantity of RNA in a population of cells. The idea that the gene is actually being up-regulated at the time of the experiment is an inference; however, reservoirs of mRNA may exist and that possibility should be considered for the system of interest. It is also important to examine the purpose of your experiment – do you want to find rare variants of a certain gene, or differential expression across the genome? This will determine the differential expression package, normalization methods, and depth of reads you will need to get reasonably accurate results.  

Biasing events can occur at every experimental step, and should be considered carefully. For instance, amplification steps or injection of cells into an in vivo environment should be considered potential sources of error. Baseline differential expression in a time course experiment should be collected if possible. 

Data

Data will come in text files from the sequencing system, usually in a FASTQ format. These contain lines in a four-line format that includes:
	quality score for each base
	base calls (the sequence)
	e.g.
o	>
o	AASKGNAH&^A
o	ATGCGTCATAG
o	+

Trimming and Normalization

Once counts of sequences in the raw data have been (collated?) compiled, sequences with counts under a certain threshold should be removed from the data set, since lowly expressed genes will skew the normalization and differential expression analysis processes. For instance, a gene with a count of one in one sample, and zero in another will appear to be hugely differentially expressed compared to a gene with thousands of counts and a 50% difference between conditions; however, genes with low counts are highly subject to error in amplification and sequencing. Some differential expression packages automatically trim any sequence with a count under 10. Experimenting with the threshold will show the plateau for the number of genes found differentially expressed.

Normalization of counts is important to remove bias between samples. For instance, one sample may have undergone longer amplification, and therefore has proportionally higher counts across all sequences.  Normalization usually examines this proportion and then corrects each sample to be proportionally 1, for instance by multiplication of the mean number of counts per sequence in each sample of a normalization factor to move the mean counts toward the same mean as in other samples.

Differential expression

Differential expression methods then compare the counts between two conditions. These 
