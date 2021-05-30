# Influence of microbiota on the effectiveness of immunotherapeutic drugs in the treatment of metastatic solid tumors

Authors: Kupaeva D., Soghomonyan K. S.
Supervisor: Sidorenko S.V.

This repository contains materials prepared by students of the Institute of Bioinformatics in the course of work on a semester project devoted to the analysis of the fecal microbiota of cancer patients.

## Introduction

Tumor cells use immune checkpoint pathways to evade the host's immune system and suppress immune cell function. The use of immune checkpoint inhibitors can suppress this signal. This type of therapy can be an effective strategy for the treatment of patients with solid metastatic tumors. However, the outcome of immunotherapy is difficult to predict, since there are currently not enough prognostic biomarkers known. Fecal microbiota can be considered as one of the prognostic markers and even as a factor in the success of therapy.
The generally accepted standard for the analysis of fecal microbiota is the analysis of the composition of the operating taxonomic units (OTU) of the microbiome based on 16S amplicon sequencing. The most commonly used packages are DADA2 and QIIME2. Although analysis of the microbiome using shotgun sequences allows for more reliable determination of taxonomic composition, gene sequences in plasmids, and genetic variation, amplicon sequencing is much cheaper and methodologically more accessible for mainstream use. The analysis of taxonomic diversity makes it possible to identify differences at the level of alpha and beta diversity of communities, to identify influential taxa, and to plan functional experiments, including those involving the transfer of fecal microbiota.
For some taxa, the correlation of bacterial biomass with progress in tumor treatment is already known. Thus, *Bifidobacterium spp* correlates with increased tumor infiltration with CD8+ T cells, and artificial administration of *Bifidobacterium spp* to mice that did not respond to therapy increases the effectiveness of therapy. The fecal microbiota of patients with metastatic melanoma responding to ipilimumab therapy is enriched in *Faecalibacterium prausnitzii*, *Gemmiger formicilis*, and *butyrate-producing bacterium SS2-1*. Today, many correlations are known between individual taxa and the effectiveness of therapy - however, these correlations are rarely reproduced in patients with different therapies and different types of tumors.
In this work, we analyzed the composition of the fecal microbiota and looked for correlations in patients with severe metastatic tumors. The unifying factor of the patients was that they all received checkpoint immunotherapy. A serious complicating factor in this study was the heterogeneity of the sample: different diagnoses, different variants of histology, the use of different inhibitors.

## Objective of the project
To determine the prognostic and predictive value of the taxonomic composition of the microbiome of patients on the results of treatment of cancer patients
## Tasks:
+ study the methods of data analysis of sequencing of the 16S rDNA fragment of the microbiome
+ evaluate the quality of raw sequencing data
+ assess taxonomic diversity (OTU, ASV) of the gut microbiome of patients
+ statistical analysis based on patient metadata and patient microbiome characteristics
+ to identify correlations between the characteristics of the microbiome and the response to immunotherapy in patients with lung cancer

## What was done
+ analysis of taxonomic diversity (OTU / ASV) of fecal microbiome of patients
  *dada2 v (1.16)., Qiime2 v.2021-02*
+ normalization of quantitative data of diversity
  *DESeq2  v.(3.11)*
+ analysis of environmental metrics
  *Qiime2 v.2021-02*
+ search for the most influential taxa and metadata, predicting the outcome of therapy using the most influential predictors
  *k-NN + LogitBoost, sklearn.linear_model.LogisticRegression,  sklearn.ensemble.RandomForestClassifier, skrearn.feature_selection, Logitboost & GradientBoostingClassifier and others.*
  
## Repository composition
1.  qiime_usage.pdf - commands used when working with qiime and examples of the results obtained
2.  dada2_workflow.R - code used to run the taxonomic estimate with dada2 and normalize the results using deseq2
3.  Phyloseq_obj.Rmd - code for processing metagenomic data obtained in dada2 using the phyloseq package
4.  ML_with_normalized_in_Deseq2_data.ipynb - ML analisys of data from dada2-phyloseq-deseq2 pipeline
5.  dada2_phyloseq_img - folder with images from dada2-phyloseq pipeline
6.  metadata_preprocessing.ipynb - code used to prepare diversity data and metadata for further work
7.  data_ml_analysis.ipynb -the code used to analyze the received data using machine learning methods
8.  Sogomonyan_Kupaeva__spring_2021.pdf - detailed presentation with all the results obtained
9.  Sogomonyan_Kupaeva__spring_2021.doc - abstract description of the results

## Summary of results
Despite our approaches, we were unable to find significant differences in fecal microbiota that would allow us to predict differences in response to therapy. The fecal microbiota of patients with different types of response to therapy does not differ in either the alpha or beta diversity of the community.
Analysis of the differential abundance of taxa reveals only one taxon: Anaerosinus glycerini. According to our data, the number of representatives of this taxon is higher in patients who did not respond to therapy, and this taxon has already been identified as correlating with the effectiveness of therapy in patients with metastatic gastric cancer. However, according to the data on biomass accumulation with a change in the proportion of the sample, this taxon makes it possible to distinguish only a small proportion of patients. In doing so, we found differentially present taxa, as well as differences in the alpha diversity of the community in patients with different types of cancer.
<img src="https://github.com/kupaeva/BI_gut_microbiota/blob/main/taxon_analysis.png" width="700" height="700">
The use of machine learning methods, however, allowed us to build a model that, with a sufficiently high reliability (accuracy 0.75 when using Logitboost linear regression based on quantitative dada2 data, normalized deseq2), can predict the treatment outcome based on quantitative and qualitative data on the composition of fecal microbiota. Analysis of the most influential predictors of the model reveals taxa for which correlations with the success of therapy are already known (Ruminococacceae, Carnobacteriaceae and Bacterioaceae, etc.). However, the list of predictors is not reproducible when using a different set of methods.

## Conclusion
We were unable to identify strong correlations or significant differences between the taxonomic composition of the fecal microbiota of patients and the effectiveness of treatment control points. We believe that the most likely reasons for this are the heterogeneity of patient diagnoses and the use of therapy that blocks different types of receptors.

## Reference
1.  Immune-Checkpoint Blockade Therapy in Lymphoma. Kuzume A, Chi S, Yamauchi N, Minami Y. Int J Mol Sci. 2020 Jul 30;21(15):5456. doi: 10.3390/ijms21155456.
2.  Schwartz DJ, Rebeck ON, Dantas G. Complex interactions between the microbiome and cancer immune therapy. Crit Rev Clin Lab Sci. 2019 Dec;56(8):567-585. doi: 10.1080/10408363.2019.1660303. Epub 2019 Sep 17. PMID: 31526274; PMCID: PMC6776419.
3.  Lin XH, Huang KH, Chuang WH, et al. The long term effect of metabolic profile and microbiota status in early gastric cancer patients after subtotal gastrectomy. PLoS One. 2018;13(11):e0206930. Published 2018 Nov 5. doi:10.1371/journal.pone.0206930
4.  Bolyen E, Rideout JR, Dillon MR, et al. 2019. Reproducible, interactive, scalable and extensible microbiome data science using QIIME 2. Nature Biotechnology 37: 852–857. https://doi.org/10.1038/s41587-019-0209-9
5.  Callahan BJ, McMurdie PJ, Rosen MJ, et al. DADA2: high‐resolution sample inference from Illumina amplicon data. Nat Methods. 2016;13:581‐583.
6.  Katoh K, Misawa K, Kuma K, et al. MAFFT: a novel method for rapid multiple sequence alignment based on fast Fourier transform. Nucleic Acids Res. 2002;30:3059‐3066.
7.  Faith DP. Conservation evaluation and phylogenetic diversity. Biol Cons. 1992;61:1‐10.
8.  Lozupone CA, Hamady M, Kelley ST, et al. Quantitative and qualitative beta diversity measures lead to different insights into factors that structure microbial communities. Appl Environ Microbiol. 2007;73:1576‐1585.
9.  Lozupone C, Knight R. UniFrac: a new phylogenetic method for comparing microbial communities. Appl Environ Microbiol. 2005;71:8228‐8235.
10.  Bokulich NA, Kaehler BD, Rideout JR, et al. Optimizing taxonomic classification of marker‐gene amplicon sequences with QIIME 2’s q2‐feature‐classifier plugin. Microbiome. 2018a;6:90.
11.  Bokulich NA, Dillon MR, Zhang Y, et al. q2‐longitudinal: Longitudinal and paired‐sample analyses of microbiome data. mSystems. 2018b;3:e00219‐e318.
12.  Love MI, Huber W, Anders S (2014). “Moderated estimation of fold change and dispersion for RNA-seq data with DESeq2.” Genome Biology, 15, 550. doi: 10.1186/s13059-014-0550-8.



