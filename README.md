# About Team Genomics_two_C
Hii all! Meet Team Genomics_two_C ! We are a highly enthusiast team of 14 members from diverse background, but what draws us together is our common interest in genomics.

# HackBio Internship 2021 Stage_2 Task
- Replicate a bioinformatic tutorial that relates to team biostack, i.e., genomics.
- Advertise about the tutorial on #transfer-market channel on Slack through quick and simple design.
- Make a comprehensive markdown of the tutorial steps.

## Project Title: Mutation calling, viral genome reconstruction and lineage/clade assignment from SARS-CoV-2 sequencing data.
Tutorial Link: https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html 

### Project Description
Massive amount of sequencing data that are generated and analysed in real-time can be used to effectively monitor higly infectious disease such as the ongoing COVID-19 pandemic. This effective monitoring allows researchers to track the emergence and transmission of mutants and comprehend the evolutionary dynamics as well.
SARS-CoV-2 sequence data is primarily generated using two sequencing platforms - Illumina and Oxford Nanopore, and various established library preparation procedures like Ampliconic and Metatranscriptomic. However, these data has no meaning in itself, unless it is analysed.
Thus, the Galaxy community will be used because it has high-quality analysis workflows to support sensitive identification of SARS-CoV-2 allelic variants (AVs) starting with allele frequencies as low as 5% from deep sequencing reads, generate user-friendly reports for batches of results and generate reliable and configurable consensus genome from called variants.

### Aim
Through this genomic analysis, team Genomics_two_C aims to extract annotated allelic variants in SARS-Cov-2 sequences and identify SARS-CoV-2 lineages using different tools and workflows in Galaxy.

### Workflow

![image](https://user-images.githubusercontent.com/88307823/130225895-3324abe4-8f54-43df-821d-b50144321510.png)

**Step1: Prepare Galaxy and data** - The sample and auxillary dataset were retrieved from [Zonedo](https://zenodo.org/record/5036687#.YR-ceo4zY2w). Auxillary dataset were used for the purpose of calling variants and annotating them.

**Step2: From FASTQ to annotated allelic variants** - In order to identify the SARS-CoV-2 allelic variants (AVs), Illumina ARTIC Workflow (also named COVID-19: variation analysis on ARTIC PE data) available on Galaxy was used on the paired-end data retrieved. It consists of a series of steps that include; quality control, trimming, mapping, deduplication, AV calling, and filtering.

**Step3: From annotated AVs per sample to AV summary** - After we have identified Annotated Variants for each sample, a “Reporting Workflow" available on Galaxy was ran on them to generate a final Annotated variants summary. This workflow takes the collection of called (with lofreq) and annotated (with SnpEff) variants (one VCF dataset per input sample) that got generated as one of the outputs of any of the four variation analysis workflows above, and generates two tabular reports and an overview plot summarizing all the variant information for our batch of samples.

**Step4: From AVs to consensus sequences** - For the variant calls, we then ran a workflow which generates reliable consensus sequences according to transparent criteria that capture at least some of the complexity of variant calling. The workflow takes a collection of VCFs and a collection of the corresponding aligned reads (for the purpose of calculating genome-wide coverage).

Next, two tools were used to assign lineages to the different samples from their consensus sequences - Pangolin and Nextclade.

**Step5: From consensus sequences to clade/lineage assignments using Pangolin** - Pangolin (Phylogenetic Assignment of Named Global Outbreak LINeages) was used to assign a SARS-CoV-2 genome sequence, the most likely lineage based on the PANGO nomenclature system. Pangolin generated a table file with taxon name and lineage assigned.

**Step6: From consensus sequences to clade/lineage assignments using Nextclade** - Nextclade assigned clades, called mutations and performed sequence quality checks on SARS-CoV-2 genomes.

**Step7: Comparing Pangolin and Nextclade assignments** - Comparision was performed between Pangolin and Nextclade clade assignments by extracting interesting columns and joining them into a single dataset using sample ids.

### Results/Conclusion
The three key results datasets produced by the reporting workflow (in step 3 above) include:

1. Combined Variant Report by Sample: This table combines the key statistics for each AV call in each sample. Each line in the dataset represents one AV detected in one specific sample

2. Combined Variant Report by Variant: This table combines the information about each AV across samples.

3. Variant frequency plot: This plot represents AFs (cell color) for the different AVs (columns) and the different samples (rows). The AVs are grouped by genes (different colors on the 1st row). Information about their effect is also represented on the 2nd row. The samples are clustered following the tree displayed on the left.

We found that Pangolin and Nextclade are globally coherent despite differences in lineage nomenclature

## Contribution

|S/N| Contributor's slack handle| Contribution|
|--|-----------------|--------------------------------------------|
|01|@Sadaf|Conceptualization of workflow|
|02|@Subhodeep, @Borode|Flyer Design|
|03|@Eslam55520, @poornima|Sample and Auxillary data retrieval|
|04|@poornima, @Sadaf|FastQC to annotated allelic variants|
|05|@Sadaf, @chimere, @Nandy| Annotated AVs per sample to AV summary|
|06|@Borode, @Rhoda, @Sadaf|AVs to consensus sequences|
|07|@Fatima, @Mohamed, @Nuiter|Consensus sequences to clade assignments with Pangolin|
|08|@Emma, @Subhodeep|Consensus sequences to clade assignments with Nextclade|
|09|@Preeti|Comparing Pangolin and Nextclade|
|10|@Iffy, @Sadaf, @Preeti|Create markdown on Github|

### References
1. Wolfgang Maier, Bérénice Batut, 2021 Mutation calling, viral genome reconstruction and lineage/clade assignment from SARS-CoV-2 sequencing data (Galaxy Training Materials). https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html Online; accessed Fri Aug 20 2021
2. Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems https://doi.org/10.1016%2Fj.cels.2018.05.012
