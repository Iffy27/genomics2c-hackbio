# HackBio Internship 2021 Stage_2 Task 🌈

- Replicate a bioinformatic tutorial that relates to team biostack, i.e., genomics.
- Advertise about the tutorial on #transfer-market channel on Slack through quick and simple design.
- Make a comprehensive markdown of the tutorial steps.

# About Team Genomics_two_C 🌈
|Team Lead - @Preeti| |Co-Lead - @Sadaf|

Hii all! Meet Team Genomics_two_C ! We are a highly enthusiast team of 14 members from diverse background; but what draws us together is our common interest in genomics.

## :computer: Project Title: Mutation calling, viral genome reconstruction and lineage/clade assignment from SARS-CoV-2 sequencing data.
Tutorial Link: https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html 

### Project Description 📝
Massive amount of sequencing data that are generated and analysed in real-time can be used to effectively monitor higly infectious disease such as the ongoing COVID-19 pandemic. This effective monitoring allows researchers to track the emergence and transmission of mutants and comprehend the evolutionary dynamics as well.
SARS-CoV-2 sequence data is primarily generated using two sequencing platforms - Illumina and Oxford Nanopore, and various established library preparation procedures like Ampliconic and Metatranscriptomic. However, these data has no meaning in itself, unless it is analysed.
Thus, the Galaxy community will be used because it has high-quality analysis workflows to support sensitive identification of SARS-CoV-2 allelic variants (AVs) starting with allele frequencies as low as 5% from deep sequencing reads, generate user-friendly reports for batches of results and generate reliable and configurable consensus genome from called variants.

### Aim :dart:
Through this genomic analysis, team Genomics_two_C aims to extract annotated allelic variants in SARS-Cov-2 sequences and identify SARS-CoV-2 lineages using different tools and workflows in Galaxy.

### Workflow 👨‍💻

![image](https://user-images.githubusercontent.com/88307823/130225895-3324abe4-8f54-43df-821d-b50144321510.png)

**Step1: Prepare Galaxy and data** - The sample and auxillary dataset were retrieved from [Zonedo](https://zenodo.org/record/5036687#.YR-ceo4zY2w). Auxillary dataset were used for the purpose of calling variants and annotating them.

**Step2: From FASTQ to annotated allelic variants** - In order to identify the SARS-CoV-2 allelic variants (AVs), Illumina ARTIC Workflow (also named COVID-19: variation analysis on ARTIC PE data) available on Galaxy was used on the paired-end data retrieved. It consists of a series of steps that include; quality control, trimming, mapping, deduplication, AV calling, and filtering.

**Step3: From annotated AVs per sample to AV summary** - After we have identified Annotated Variants for each sample, a “Reporting Workflow" available on Galaxy was ran on them to generate a final Annotated variants summary. This workflow takes the collection of called (with lofreq) and annotated (with SnpEff) variants (one VCF dataset per input sample) that got generated as one of the outputs of any of the four variation analysis workflows above, and generates two tabular reports and an overview plot summarizing all the variant information for our batch of samples.

**Step4: From AVs to consensus sequences** - For the variant calls, we then ran a workflow which generates reliable consensus sequences according to transparent criteria that capture at least some of the complexity of variant calling. The workflow takes a collection of VCFs and a collection of the corresponding aligned reads (for the purpose of calculating genome-wide coverage).

Next, two tools were used to assign lineages to the different samples from their consensus sequences - Pangolin and Nextclade.

**Step5: From consensus sequences to clade/lineage assignments using Pangolin** - Pangolin (Phylogenetic Assignment of Named Global Outbreak LINeages) was used to assign a SARS-CoV-2 genome sequence, the most likely lineage based on the PANGO nomenclature system. Pangolin generated a table file with taxon name and lineage assigned.

**Step6: From consensus sequences to clade/lineage assignments using Nextclade** - Nextclade assigned clades, called mutations and performed sequence quality checks on SARS-CoV-2 genomes.

**Step7: Comparing Pangolin and Nextclade assignments** - Comparision was performed between Pangolin and Nextclade clade assignments by extracting interesting columns and joining them into a single dataset using sample ids.

### Results/Conclusion 📗

- Result of step one is contained in the link below.\
<https://github.com/Iffy27/genomics2c-hackbio/blob/main/Results%20workflow%201%20step%201.zip>

- The dataset produced by the reporting workflow  include a variant frequency plot. This plot represents AFs (cell color) for the different AVs (columns) and the different samples (rows). The AVs are grouped by genes (different colors on the 1st row). Information about their effect is also represented on the 2nd row. The samples are clustered following the tree displayed on the left.

<img src= "https://user-images.githubusercontent.com/71774308/130228701-444375b9-d1cf-437c-8cdc-b1cebc6157aa.jpg" alt="design" height = "500" width = "1000"/>

- **Lineage from Pangolin**

B.1.1.7		14\
B.1.525		1\
B.1.617.2 	3

- **Lineage from Nextclade**

20I (Alpha, V1)	14\
21A (Delta)	3\
21D (Eta)	1


- **Result_Comparison between nextclade and pangolin output**

![Comparison between Pangolin and Nextclade clade assignments](https://user-images.githubusercontent.com/88307823/130308785-41dc5be8-9f04-4329-a573-ac0df83c24bc.jpg)

From the results, we found that Pangolin and Nextclade are globally coherent despite differences in lineage nomenclature.

## Team Work 🤜🤛

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
|11|@Nuiter|Workflow Video Creation|

### References 📚
\[1] Budd, J., Miller, B.S., Manning, E.M., Lampos, V., Zhuang, M., Edelstein, M. et al. (2020). Digital technologies in the public-health response to COVID-19. *Nature Medicine* **26**, 1183-1192.\
\[2] Ting, D.S., Carin, L., Dzau, V. and Wong, T.Y. (2020). Digital technology and COVID-19. *Nature Medicine* **26**, 459-461.\
\[3] Wolfgang Maier, Bérénice Batut, 2021 Mutation calling, viral genome reconstruction and lineage/clade assignment from SARS-CoV-2 sequencing data (Galaxy Training Materials). https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html Online; accessed Fri Aug 20 2021\
\[4] Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems https://doi.org/10.1016%2Fj.cels.2018.05.012\
\[5]<https://www.biocommons.org.au/events/galaxy-sars-cov2>\
\[6] <https://pha4ge.org/sars-cov-2-data-analysis-and-monitoring-with-galaxy/>\
\[7] <https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html#prepare-galaxy-and-data>



# 🍁🍁🍁 THANK YOU 🍁🍁🍁
