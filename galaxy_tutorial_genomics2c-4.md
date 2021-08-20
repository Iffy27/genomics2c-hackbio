##              Hackbio Stage Two Project for \#Genomics_two_C 

# Project Title: Mutation calling, viral genome reconstruction and lineage/clade assignment from SARS-CoV-2 sequencing data

**Tutorial Link**: [Mutation calling, viral genome reconstruction and lineage/clade assignment from SARS-CoV-2 sequencing data (galaxyproject.org)](https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html#prepare-galaxy-and-data)

## Graphical Abstract

<img src= "https://user-images.githubusercontent.com/71774308/129928073-cd099942-3920-417c-8048-43c3a94c1eff.png" alt="design" width = "500"/>

## Introduction 

Effectively monitoring global infectious disease crises, such as the COVID-19 pandemic, requires capacity to generate and analyze large volumes of sequencing data in near real time.

These data have proven essential for monitoring the emergence and spread of new variants, and for understanding the evolutionary dynamics of the virus. Two sequencing platforms (Illumina and Oxford Nanopore) in combination with several established library preparation (Ampliconic and metatranscriptomic) strategies are predominantly used to generate SARS-CoV-2 sequence data. However, these data need to be analyzed.

For this research, The Galaxy community will be used because it has high-quality analysis workflows to support sensitive identification of SARS-CoV-2 allelic variants (AVs) starting with allele frequencies as low as 5% from deep sequencing reads, generate user-friendly reports for batches of results and generate reliable and configurable consensus genome  from called variants

## Aim

The aim of this research is to extract annotated allelic variants in SARS-Cov-2 sequences and identify SARS-CoV-2 lineages using different tools and workflows in Galaxy. Team Genomics_two_c will be extracting annotated allergic variants in SARS-Cov-2 sequences to identify SARS-Cov-2 lineages using different tools and workflows in Galaxy.

## Objectives:

- SARS-CoV-2 data preparation
- Select and run workflow to extract annotated allelic variants from FASTQ files
- Run workflow to summarize and generate report for previously called allelic variants
- Interpret summaries for annotated allelic variants
- Run workflow to extract consensus sequences
- Select and run tools to assign clades/lineages

## Methodology/ Workflow

**1. Prepare Galaxy and data**

•	Get sequencing data -Here, dataset present in Galaxy and stored on [Zenodo](https://zenodo.org/record/5036687) were retrieved using the following URLs;

> `https://zenodo.org/record/5036687/files/ERR5931005_1.fastqsanger.gz
> https://zenodo.org/record/5036687/files/ERR5931005_2.fastqsanger.gz
> https://zenodo.org/record/5036687/files/ERR5931006_1.fastqsanger.gz
> https://zenodo.org/record/5036687/files/ERR5931006_2.fastqsanger.gz
> https://zenodo.org/record/5036687/files/ERR5931007_1.fastqsanger.gz`

Find full list of URLs at <https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html#prepare-galaxy-and-data>

• Import auxiliary datasets- For the purpose of calling variants and annotating them, the following datasets were imported;
>   - the SARS-CoV-2 reference (`NC_045512.2_reference.fasta`)
>   - gene product name aliases (`NC_045512.2_feature_mapping.tsv`)
>   - ARTIC v3 primer scheme (`ARTIC_nCoV-2019_v3.bed`)
>   - ARTIC v3 primer amplicon grouping info ('ARTIC_amplicon_info_v3.tsv') 

**2. From FASTQ to annotated allelic variants**

In order to identify the SARS-CoV-2 allelic variants (AVs), Illumina ARTIC Workflow (also named `COVID-19: variation analysis` on ARTIC PE data) available on Galaxy was used on the paired-end data retrieved. It consists of a series of steps that include; quality control, trimming, mapping, deduplication, AV calling, and filtering.

**3. From annotated AVs per sample to AV summary**

After we have identified Annotated Variants for each sample, a “Reporting Workflow" available on Galaxy was ran on them to generate a final Annotated variants summary. This workflow takes the collection of called (with lofreq) and annotated (with SnpEff) variants (one VCF dataset per input sample) that got generated as one of the outputs of any of the four variation analysis workflows above, and generates two tabular reports and an overview plot summarizing all the variant information for our batch of samples. 

**4. From AVs to consensus sequences**

For the variant calls, we then ran a workflow which generates reliable consensus sequences according to transparent criteria that capture at least some of the complexity of variant calling. The workflow takes a collection of VCFs and a collection of the corresponding aligned reads (for the purpose of calculating genome-wide coverage).

**5. From consensus sequences to clade/lineage assignments**

To assign lineages to the different samples from their consensus sequences, two available tools: Pangolin and Nextclade were used.

-	With Pangolin
Pangolin (Phylogenetic Assignment of Named Global Outbreak LINeages) were used to assign a SARS-CoV-2 genome sequence, the most likely lineage based on the PANGO nomenclature system. Pangolin generated a table file with taxon name and lineage assigned.

-	With Nextclade
Nextclade assigned clades, called mutations and performed sequence quality checks on SARS-CoV-2 genomes.

-	Comparison between Pangolin and Nextclade assignments
We compared Pangolin and Nextclade clade assignments by extracting interesting columns and joining them into a single dataset using sample ids. 

## Results and Discussion

- Result of step one is contained in the link below.\
<https://github.com/Iffy27/genomics2c-hackbio/blob/main/Results%20workflow%201%20step%201.zip>

- The dataset produced by the reporting workflow  include a variant frequency plot. This plot represents AFs (cell color) for the different AVs (columns) and the different samples (rows). The AVs are grouped by genes (different colors on the 1st row). Information about their effect is also represented on the 2nd row. The samples are clustered following the tree displayed on the left.

<img src= "https://user-images.githubusercontent.com/71774308/130228701-444375b9-d1cf-437c-8cdc-b1cebc6157aa.jpg" alt="design" height = "500" width = "1000"/>

- **Result_Comparison between nextclade and pangolin output**

ERR5931005	21A (Delta)	ERR5931005	B.1.617.2	Delta (B.1.617.2-like)\
ERR5931006	21A (Delta)	ERR5931006	B.1.617.2	Delta (B.1.617.2-like)\
ERR5931007	20I (Alpha, V1)	ERR5931007	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5931008	21A (Delta)	ERR5931008	B.1.617.2	Delta (B.1.617.2-like)\
ERR5949456	20I (Alpha, V1)	ERR5949456	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949457	20I (Alpha, V1)	ERR5949457	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949458	20I (Alpha, V1)	ERR5949458	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949459	20I (Alpha, V1)	ERR5949459	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949460	21D (Eta)	ERR5949460	B.1.525	Eta (B.1.525-like)\
ERR5949461	20I (Alpha, V1)	ERR5949461	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949462	20I (Alpha, V1)	ERR5949462	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949463	20I (Alpha, V1)	ERR5949463	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949464	20I (Alpha, V1)	ERR5949464	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949465	20I (Alpha, V1)	ERR5949465	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949466	20I (Alpha, V1)	ERR5949466	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949467	20I (Alpha, V1)	ERR5949467	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949468	20I (Alpha, V1)	ERR5949468	B.1.1.7	Alpha (B.1.1.7-like)\
ERR5949469	20I (Alpha, V1)	ERR5949469	B.1.1.7	Alpha (B.1.1.7-like)

- **Lineage from Pangolin**

B.1.1.7		14\
B.1.525		1\
B.1.617.2 	3\


- **Lineage from Nextclade**

20I (Alpha, V1)	14\
21A (Delta)	3\
21D (Eta)	1

From the results, we found that Pangolin and Nextclade are globally coherent despite differences in lineage nomenclature

## Bibliography
\[1] Budd, J., Miller, B.S., Manning, E.M., Lampos, V., Zhuang, M., Edelstein, M. et al. (2020). Digital technologies in the public-health response to COVID-19. *Nature Medicine* **26**, 1183-1192.\
\[2] Ting, D.S., Carin, L., Dzau, V. and Wong, T.Y. (2020). Digital technology and COVID-19. *Nature Medicine* **26**, 459-461.\
\[3] <https://www.biocommons.org.au/events/galaxy-sars-cov2>\
\[4] <https://pha4ge.org/sars-cov-2-data-analysis-and-monitoring-with-galaxy/>\
\[5] <https://training.galaxyproject.org/training-material/topics/variant-analysis/tutorials/sars-cov-2-variant-discovery/tutorial.html#prepare-galaxy-and-data>
