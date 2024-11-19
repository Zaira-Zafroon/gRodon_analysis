# gRodon_analysis

My process:
1. The first thing is to take reads and then make it megahit for assembly. Malte has done this so I won't. Need confirmations.

2. Do gene calls. Here is where things get tricky. Now, Either I use the prokka anaylsis pipeline or the prodigal pipeline. I believe the gene calls are from the prodigal here for the contigs. Then I can do blast. I talked to Malte. He said "gene_calls" files are really just very simply the output of prodigal in -meta mode" and "I filtered out small contigs < 2kb before the gene calling". So, based on this AND THE LITERATURE THAT SUGGEST GEETING RID OF small contigs before gene calling is great I can go ahead with Prodigal.

3.Then once I have the regions,I would still need to do my read files.The clean read files will be mapped to genes and I get relative coverage abunance tvs. I need to understand that bit more. 
4. Run gRodon 2. it seems 1 core, should be enough. just make sure I can write a script for submitting.
5. Get the results. 
6. Then I do my analysis.
7.Cross validate with growthpred.

#Infornation dump :
Users should be cutious when interpreting results for organisms with predicted doubling times greater than 5 hours -point noted
First thing is t figure out, where the gene calls are from. If they are from the whole contigs I am great.
I can use that, run blast and then be done.
if not, I need to use Prokka to aanlyze it.
Also, I need to do the coverage stuff.
I can try to do the weighted vs unweighted first, Then based on results i Cna do a collreaton analysis and do the rest of my code.

Total runtime for 1,000 metagenomes (on a single core):

Total time=1,000 ×114=114,000 seconds (114 seconds on average per genme/1.9 min)
Number of cores required:

Cores
=Total time /Available time = 114,000/259,200≈ 0.44.

temparature is an optional predictor here. we dont know temparature or we can chck as well.Dont know what would be great here 
Temperature as a Variable: If you have information on the optimal growth temperatures of the microbial species present in your samples or if you can estimate the environmental temperatures during sample collection, consider including this as a variable in your analysis. This can enhance the accuracy of your growth rate predictions.

Deafult mode:a lready takes away the shorter gene(messes up predictions) and the assmebly is reired before gene calling which is what I am doing . 
Remeber the human micro-biome generally being composed of much-faster-growing organisms living under nu-trient-rich conditions.
The overlap, despite some statistical differences, suggests that environmental factors significantly influence codon usage patterns - this is important when I am writing.
we can run this too if you want 
For comparisons, growthpred v1.0.8 was run from a docker image from the work of Long et al. (25)
(https://hub.docker.com/r/shengwei/growthpred) in metagenome mode (-m) using the same set of ribo-
somal proteins as those for gRodon in all cases. But it should have better be less
Actual to follow:
Raw reads and assemblies for the HSASM data set (8) were obtained from https://www.hmpdacc.org/
hmp/HMASM/#data, and sample temperature was assumed to be 37°C. Assemblies were annotated with
prokka (using options –norrna –notrna –metagenome –centre X –compliant [46]). For reads, adapters
and low-quality reads were trimmed using fastp v0.21.0 (47), and then cleaned reads were mapped to
inferred genes using bwa mem v0.7.12 (default settings [48]) and coverage was quantiﬁed using bamcov
v0.1.1 (available at https://github.com/fbreitwieser/bamcov).

Synthetic Community:
Synthetic metagenomes. Synthetic reads were generated from genome mixtures using inSilicoSeq
(36). We (using options –n_reads 100M –model hiseq –coverage lognormal) generated synthetic metage-
nomes with a Hi-Seq sequencing error model and 100 	 2 million 125-bp paired reads. Adapters and low-
quality reads were trimmed using fastp v0.21.0, and then either reads were assembled with MEGAHIT v1.2.9
(default parameters [49]) and genes were annotated with prokka (using options –norrna –notrna –metage-
nome –centre X –compliant [46]) or genes were called directly from reads using FragGeneScanRs (using
option –training-ﬁle illumina_5 [50, 51]). For assemblies, cleaned reads were mapped to inferred genes using
bwa mem v0.7.12 (default settings [48]), and coverage was quantiﬁed using bamcov v0.1.1 (available at
https://github.com/fbreitwieser/bamcov). We annotated genes called directly from reads as ribosomal pro-
teins using blastn (E value cutoff of 1025 and a 99% identity [52]) and the ribosomal protein database from
growthpred (13). The sets of genes predicted directly from reads were very large (160 million genes on average-
age), so that we subsampled 1% of genes per sample for gRodon prediction (increasing this to 10% did not
change our result; see Fig. S21 at https://doi.org/10.6084/m9.ﬁgshare.20440377.v1).


