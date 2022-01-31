# EMBL-EBI Virtual Course: 💻 [SymbNET](https://www.ebi.ac.uk/training/events/symbnet-2022/) 🧬 From Metagenomics to Metabolic Interactions (Day 5)

## 💰 Learning Outcomes

 - Generate genome-scale metabolic models (GEMs) from metagenome assembled genomes (MAGs)
 - Predict metabolic interactions within bacterial communities
 - Characterize communities using competition-cooperation plot
 - Explore uncertainty in GEM reconstruction and simulation
 - Pros and cons of using reference genomes vs metagenome-assembled or single-amplified genomes for metabolic modeling 

## 🍬 Software

| Tool | Task | GitHub | Reference |
| :---         | :---           | :---          |  :---         | 
| CarveMe   | Build GEMs from MAGs   |[Repo](https://github.com/cdanielmachado/carveme)    |        [Paper](https://academic.oup.com/nar/article/46/15/7542/5042022)       |
| SMETANA     | Predict metabolic interactions between GEMs       | [Repo](https://github.com/cdanielmachado/smetana)      |          [Paper](https://www.pnas.org/content/112/20/6449)     |
| metaGEM   | Metagenomic metabolic modeling workflow | [Repo](https://github.com/franciscozorrilla/metaGEM)    | [Paper](https://academic.oup.com/nar/article/49/21/e126/6382386)    |
| Snakemake   | Workflow management and reproducibility    | [Repo](https://github.com/snakemake/snakemake)    | [Paper](https://f1000research.com/articles/10-33)   |

Pictured below is the metaGEM workflow for reconstructing and simulating metagenome based metabolic models. This training module will focus on how to generate and simulate communities of metabolic models using CarveMe and SMETANA.

![](https://github.com/franciscozorrilla/SymbNET/blob/main/plots/metaGEM/metagem_fig1.png)

## 🗻 Contents

 - `/genomes/` ORF annotated protein fasta files (.faa)
 - `/models/` pre-generated CarveMe GEMs for simulation (.xml)
 - `/ensembles/` pre-generated ensemble models for network uncertainty (.xml) 
 - `/simulations/` pre-computed SMETANA simulations (.tsv)
 - `/data/` various metadata, taxonomic assignments, media files, etc.
 - `/scripts/` markdown, r-markdown, and jupyter notebooks for each exercise
 - `/plots/` visualization of results 

## ☑️ Exercises
### Part I
 0. [Start by cloning this repo](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/0.clone_repo.md)
 1. [Use CarveMe to generate GEMs for a bacterial community](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/1.carve_models.md)
 2. [Visualize model metrics across species](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/2.plot_gut_model_summary.ipynb)
 3. [Use SMETANA detailed algorithm to predict metabolic interactions between species](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/3.run_smetana_detailed_interactions.md)
 4. [Visualize detailed interactions with alluvial diagrams](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/4.plot_smetana_detailed_interactions.md)

### Part II
 5. [Use SMETANA global algorithm to generate MIP & MRO metrics for community of GEMs](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/5.run_smetana_global_metrics.md)
 6. [Visualize communities on cooperation-competition plot](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/6.plot_competition_cooperation.ipynb)
 7. [Generate ensemble models (optional)](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/7.generate_ensemble_models.md)
 8. [Quantify network uncertainty (optional)](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/8.plot_ensemble_dist.ipynb)
 9. [Discussion of methods, results, and interpretation](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/9.wrap_up_discussion.md)

## ⛏️ Datasets

The following table describes in detail the 6 small bacterial communities of 5 species that we will consider for metabolic modeling. These include MAG,SAG, and reference genome-based communities; the samples also span the human gut, kefir, and soil habitats.

| Microbiome |Genome type| Condition | Species | Links |
| :---        | :--- | :---           | :---          |  :---         | 
| Human gut  | MAGs |Normal Glucose Tolerance (NGT, ERR260255) |  <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>   | <ul><li>[Paper](https://www.nature.com/articles/nature12198)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/analyses/MGYA00001287#overview)</li></ul> |
| Human gut   | MAGs |Impaired Glucose Tolerance (IGT, ERR260172)      | <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>   |  <ul><li>[Paper](https://www.nature.com/articles/nature12198)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/analyses/MGYA00001094?version=1.0#overview)</li></ul> |
| Human gut  | MAGs | Type II Diabetes (T2D, ERR260140)  | <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>  | <ul><li>[Paper](https://www.nature.com/articles/nature12198)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/analyses/MGYA00001062?version=1.0#overview)</li></ul> |
| Human gut| Reference genomes | Reference genomes taken from RefSeq   | <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>  | <ul><li>[NCBI](https://www.ncbi.nlm.nih.gov/)</li></ul>   |
| Kefir | SAGs | Fermented with German grains (GER6)    | <ul><li>*L. mesenteroides*</li><li>*L. lactis*</li><li>*A. fabarum*</li><li>*L. kefiranofaciens*</li><li>*L. kefiri*</li></ul>  | <ul><li>[Paper](https://www.nature.com/articles/s41564-020-00816-5)</li></ul>   |
| Soil | MAGs |  Calcarosols from Uluru, Australia (ERR671933)   | <ul><li>f_Thermoleophilaceae</li><li>f_Herpetosiphonaceae</li><li>f_Phormidiaceae</li><li>f_Geodermatophilaceae</li><li>f_Rubrobacteraceae</li></ul>   | <ul><li>[Paper](https://academic.oup.com/gigascience/article/5/1/s13742-016-0126-5/2720982)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/studies/MGYS00000434)</li></ul>  |

## 🏄 Metabolic modeling repos

### Tools

 - [metaGEM](https://github.com/franciscozorrilla/metaGEM): Reconstruction and simulation of genome scale metabolic models directly from metagenomes
 - [DesignMC](https://github.com/cdanielmachado/designmc): Design microbial communities for production of specific target compounds using GEMs 
 - [HiOrCo](https://github.com/cdanielmachado/HiOrCo): Compute higher order cooccurence using abundance across samples
 - [Reframed](https://github.com/cdanielmachado/reframed): Metabolic modeling package

### Resources

 - [metaGEM_paper](https://github.com/franciscozorrilla/metaGEM_paper): metaGEM paper results
 - [metaGEM_unseenbio](https://github.com/franciscozorrilla/unseenbio_metaGEM): metaGEM analysis of unseen bio at-home-test WGS sequencing data
 - [Cooccurrence paper](https://github.com/cdanielmachado/cooccurrence): Supplement repo to cooccurrence paper
 - [CarveMe paper](https://github.com/cdanielmachado/carveme_paper): Supplement repo to CarveMe paper
 - [Kefir paper](https://github.com/cdanielmachado/kefir_paper): Supplement repo to kefir paper
 - [EMBL GEMs](https://github.com/cdanielmachado/embl_gems): Collection of RefSeq-based GEMs

Please cite literature if you make use of relevant tools and/or resources.

## 📚 Suggested Reading

 - [Intro to FBA](https://www.nature.com/articles/nbt.1614): What is flux balance analysis?
 - [CarveMe](https://academic.oup.com/nar/article/46/15/7542/5042022): Fast automated reconstruction of genome-scale metabolic models for microbial species and communities
 - [SMETANA](https://www.pnas.org/content/112/20/6449): Metabolic dependencies drive species co-occurrence in diverse microbial communities
 - [metaGEM](https://academic.oup.com/nar/article/49/21/e126/6382386): Reconstruction of genome scale metabolic models directly from metagenomes
 - [Human gut study](https://www.nature.com/articles/s41564-018-0123-9): Nutritional preferences of human gut bacteria reveal their metabolic idiosyncrasies
 - [Kefir study](https://www.nature.com/articles/s41564-020-00816-5): Metabolic cooperation and spatiotemporal niche partitioning in a kefir microbial community
 - [Cooccurrence study](https://www.nature.com/articles/s41559-020-01353-4): Polarization of microbial communities between competitive and cooperative metabolism

## 🚛 Software requirements

 - [CarveMe](https://github.com/cdanielmachado/carveme)
 - [SMETANA](https://github.com/cdanielmachado/smetana)

### Dependencies

 - [IBM CPLEX Solver (academic edition)](https://community.ibm.com/community/user/datascience/blogs/xavier-nodet1/2020/07/09/cplex-free-for-students)
 - [Diamond](https://github.com/bbuchfink/diamond)

### Additonal packages
 
 - [Prodigal](https://github.com/hyattpd/Prodigal)
 - [Git](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)
 - [R (v4.x)](https://cran.r-project.org/)
   * [tidyverse](https://github.com/tidyverse/tidyverse)
   * [ggalluvial](https://github.com/corybrunson/ggalluvial/)
   * [ggpubr](https://cran.r-project.org/web/packages/ggpubr/index.html)
   * [Rstudio](https://www.rstudio.com/)
 - [Python (v3.x)](https://www.python.org/downloads/)
   * [framed](https://github.com/cdanielmachado/framed)
   * [reframed](https://github.com/cdanielmachado/reframed)
   * [matplotlib](https://matplotlib.org/)
   * [seaborn](https://seaborn.pydata.org/)
   * [pandas](https://github.com/pandas-dev/pandas)
   * [glob](https://docs.python.org/3/library/glob.html)
   * [numpy](https://numpy.org/)
   * [random](https://docs.python.org/3/library/random.html)
   * [scipy](https://scipy.org/)
   * [jupyter notebook](https://jupyter.org/install)

## 🇪🇺 About SymbNET

SymbNET is a European network for host-microbe interactions research, funded by the European Union’s Horizon 2020 research and innovation programme. The project coordinated by FCG-IGC (Instituto Gulbenkian de Ciência, Portugal), brings together the world-leading research institutions EMBL (European Molecular Biology Laboratory, Germany),  CAU (Christian-Albrechts-Universität zu Kiel, Germany),  and UNIL (Université de Lausanne,  Switzerland), and a local widening partner ITQB NOVA (Instituto de Tecnologia Química e Biológica, Portugal).

This project has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement Nº 952537
