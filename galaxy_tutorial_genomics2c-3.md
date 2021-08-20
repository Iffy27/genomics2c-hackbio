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

- **Pangolin-output**

|ERR5931005|B.1.617.2|0.0|0.959925523199523|Delta (B.1.617.2-like)|passed_qc|scorpio call: Alt alleles 13; Ref alleles 0; Amb alleles 0; Oth alleles 0|
|-----------|-----------|----|----------------------|---------------------------------|-----------|----------------------------------------------------------------------------------------|
|ERR5931006|	B.1.617.2|	0.0|	0.999925523199523|3	Delta (B.1.617.2-like)|passed_qc	|scorpio call: Alt alleles 12; Ref alleles 0; Amb alleles 1; Oth alleles 0|
|ERR5931007|	B.1.1.7|	0.0	|0.9919297323674037|	Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 21; Ref alleles 1; Amb alleles 1; Oth alleles 0|
|ERR5931008|	B.1.617.2|	0.0	|0.990148153718884|	Delta (B.1.617.2-like)|passed_qc	|scorpio call: Alt alleles 12; Ref alleles 0; Amb alleles 1; Oth alleles 0|
|ERR5949456|	B.1.1.7|	0.0	|0.9999627629864085|	Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 21; Ref alleles 1; Amb alleles 1; Oth alleles 0|
|ERR5949457|	B.1.1.7|	0.0	|1.0	|Alpha (B.1.1.7-like)	0.956500|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949458|	B.1.1.7|	0.0	|1.0	|Alpha (B.1.1.7-like)	0.956500|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949459|	B.1.1.7|	0.0	|0.9999627629864085	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949460|	B.1.525|	0.0	|0.990186125211506	|Eta (B.1.525-like) |passed_qc	|scorpio call: Alt alleles 15; Ref alleles 0; Amb alleles 1; Oth alleles 0|
|ERR5949461|	B.1.1.7|	0.0	|0.9810676480631332	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949462|	B.1.1.7|	0.0	|0.9971246125695508	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949463|	B.1.1.7|	0.0	|0.990148153718884	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949464|	B.1.1.7|	0.0	|0.990186125211506	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949465|	B.1.1.7|	0.0	|0.9970871611023975	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 21; Ref alleles 1; Amb alleles 1; Oth alleles 0|
|ERR5949466|	B.1.1.7|	0.0	|0.9955492388824475	|Alpha (B.1.1.7-like)|passed_qc	|scorpio call: Alt alleles 21; Ref alleles 1; Amb alleles 1; Oth alleles 0|
|ERR5949467|	B.1.1.7|	0.0|0.990186125211506	|Alpha (B.1.1.7-like)|passed_qc|scorpio call: Alt alleles 22; Ref alleles 1; Amb alleles 0; Oth alleles 0|
|ERR5949468|	B.1.1.7|	0.0|	0.990072202166065	|Alpha (B.1.1.7-like)|passed_qc|scorpio call: Alt alleles 21; Ref alleles ; Amb alleles 1; Oth alleles 0|
|ERR5949469|	B.1.1.7|	0.0|	0.9938181409463864|	Alpha (B.1.1.7-like)|passed_qc|	scorpio call: Alt alleles 21; Ref alleles 1; Amb alleles 1; Oth alleles 0|

- Lineage from Pangolin

B.1.1.7		14\
B.1.525		1\
B.1.617.2 	3

- **Nextclade output**

|ERR5931005|	21A (Delta)|	0.17361111111111113|	good|G210T,C241T,C1191T,C1267T,C2334T,C3037T,C5184T,G9203A,T9678C,C11005A,C12076T,C14408T,A17496G,A20396G,C21618G,A21792C,G21987A,T22917G,C22995A,A23403G,C23604G,G24410A,C25469T,G26217T,T26767C,T27638C,C27752T,C28253T,A28461G,G28881T,G29402T,A29771G|
|-----------|---------------|-----------------------|-----|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|	
|ERR5931006|	21A (Delta)	|0.17361111111111113|	good|G210T,C241T,C1191T,C1267T,C2334T,C3037T,C5184T,G9203A,T9678C,C11005A,C12076T,C14408T,A17496G,A20396G,C21618G,A21792C,G21987A,T22917G,A23403G,C23604G,G24410A,C25469T,G26217T,T26767C,T27638C,C27752T,C28253T,A28461G,G28881T,G29402T,A29771G|	
|ERR5931007|	20I (Alpha, V1)|	0.1966700960219479|	good|C241T,C913T,C1473T,C3037T,C3267T,C5388A,C5986T,T6954C,A12594G,C14408T,C15279T,T16176C,A23063T,C23271A,A23403G,C23604A,C23709T,C23833T,T24506G,G24914C,C25578T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,G28881A,G28882A,G28883C,C28915T,C28977T|	
|ERR5931008|	21A (Delta)|	0.28226680384087793|	good|G210T,C241T,C874A,C1191T,C1267T,C3037T,C5184T,C9891T,T11418C,T12946C,C14408T,A15201G,C15371T,G15451A,C16466T,C18176T,A20262G,C21618G,G21987A,T22917G,A23403G,C23520T,C23604G,G24410A,C25469T,T26767C,T27638C,C27739T,C27752T,A28461G,G28881T,G29402T|
|ERR5949456|	20I (Alpha, V1)|	0.6944444444444445|	good|C241T,C913T,C3037T,C3267T,G4311A,C5388A,C5986T,T6954C,T8603C,C12076T,C14408T,C15279T,T16176C,C16997T,A17615G,C22480T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G25437T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,G28881A,G28882AT|	
|ERR5949457|	20I (Alpha, V1)|	1.5625|	good|C241T,C913T,C3037T,C3267T,C5388A,C5986T,G5992T,T6954C,C10156T,G12070T,C12880T,C14408T,C14676T,C15279T,T16176C,C21721T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,C28708T,G28881A,G28882A,G28883C,C28957T|
|ERR5949458|	20I (Alpha, V1)|	1.5625	good|C241T,C913T,C3037T,C3267T,C5388A,C5986T,G5992T,T6954C,C10156T,G12070T,C12880T,C14408T,C14676T,C15279T,T16176C,C21721T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,C28708T,G28881A,G28882A,G28883C,C28957T|	
|ERR5949459|	20I (Alpha, V1)|	2.777777777777778|	good|C241T,C913T,C2841T,C3037T,C3267T,C5388A,C5986T,T6954C,C7165T,C7528T,C14183T,C14408T,C14676T,C15279T,T16176C,A17615G,C18138T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G26828T,A27455G,C27688T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A|
|ERR5949460|	21D (Eta)|	2.8864334705075447|	good|C241T,G1462T,C1498T,G2659A,C3037T,C6285T,C7843T,T8593C,C9565T,C14407T,C14408T,C18171T,A20724G,A21717G,C21762T,G23012A,A23403G,G23587C,G23593C,G24124T,T24224C,C24748T,G26173T,G26209T,C26305T,T26767C,C28308G,A28699G,C28887T,G29543T|	
|ERR5949461|	20I (Alpha, V1)|	10.130209190672154|	good|C241T,C913T,C2143T,C3037T,C3267T,C4321T,C5388A,C5986T,T6954C,T8603C,C10834T,C13119T,C13329T,A13947T,C14408T,C14676T,C15279T,T16176C,A17615G,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G25437T,G25660T,C27389T,C27972T,G28048T,A28111G|	
|ERR5949462|	20I (Alpha, V1)|	2.9437585733882035|	good|C913T,C2841T,C3037T,C3267T,C5388A,C5986T,T6954C,C7165T,C7528T,C14183T,C14408T,C14676T,C15279T,T16176C,A17615G,C18138T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G26828T,A27455G,C27688T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A|	
|ERR5949463|	20I (Alpha, V1)|	2.8864334705075447|	good|C241T,C913T,C2841T,C3037T,C3267T,C5388A,C5986T,T6954C,C7165T,C7528T,C14183T,C14408T,C14676T,C15279T,T16176C,A17615G,C18138T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G26828T,A27455G,C27688T,C27972T,G28048T,A28111G,G28280C,A28281T|
|ERR5949464|	20I (Alpha, V1)|	25.106227709190673|	good|C241T,C913T,C3037T,C3267T,G3716T,C5388A,C5849T,C5986T,A6183C,A6411T,C6675T,T6954C,T8603C,C11300T,C14408T,C14676T,G15199A,C15279T,T16176C,A17615G,G20083A,T21357C,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G25186T,G25437T,G25907T,C27972T|
|ERR5949465|	20I (Alpha, V1)|	2.9437585733882035|	good|C913T,C2841T,C3037T,C3267T,C5388A,C5986T,C7165T,C7528T,C14183T,C14408T,C14676T,C15279T,T16176C,A17615G,C18138T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G26828T,A27455G,C27688T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,G28881A|
|ERR5949466|	20I (Alpha, V1)|	8.506944444444445|good|	C241T,C913T,C2143T,C3037T,C3267T,C4321T,C5388A,C5986T,T6954C,T8603C,C10834T,C13119T,C13329T,A13947T,C14408T,C15279T,T16176C,A17615G,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G25437T,G25660T,C27389T,C27972T,G28048T,A28111G,C28227T,G28280C|	
|ERR5949467|	20I (Alpha, V1)|	4.446505486968449|	good|C241T,C913T,C3037T,C3267T,C3784T,C5284T,C5388A,C5986T,T6954C,T10891C,C14408T,C14676T,C15279T,T16176C,T18417C,C18647T,A22278T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,C25836T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,G28739T,G28881A|
|ERR5949468|	20I (Alpha, V1)|	1.2034602194787383|	good|C241T,C913T,C1142T,C2880T,C3037T,C3177T,C3267T,C5388A,C5986T,T6954C,C14408T,C15279T,T16176C,C18788T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,G25088T,C25916T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,G28881A,G28882A,G28883C,C28977T|
|ERR5949469|	20I (Alpha, V1)|	3.164938271604939|	good|C241T,C913T,C3037T,C3267T,C3784T,C5284T,C5388A,C5986T,T6954C,T10891C,C14408T,C15279T,T16176C,T18417C,C18647T,A23063T,C23271A,A23403G,C23604A,C23709T,T24506G,G24914C,C25836T,C27972T,G28048T,A28111G,G28280C,A28281T,T28282A,G28739T,G28881A,G28882A,G28883C,C28977T,C29296T|	

- Lineage from Nextclade

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
