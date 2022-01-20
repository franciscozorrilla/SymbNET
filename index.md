# 💻 SymbNET 🧬 From Metagenomics to Metabolic Interactions (Day 5) 

## 💰 Learning Outcomes

 - Generate genome-scale metabolic models (GEMs) from metagenome assembled genomes (MAGs)
 - Predict metabolic interactions within bacterial communities
 - Characterize communities using competition-cooperation plot
 - Explore uncertainty in GEM reconstruction and simulation
 - Pros and cons of using reference genomes vs metagenome-assembled or single-amplified genomes for metabolic modeling 

## 🗻 Contents

 - `/genomes/` ORF annotated protein fasta files (.faa)
 - `/models/` pre-generated CarveMe GEMs for simulation (.xml)
 - `/ensembles/` pre-generated ensemble models for network uncertainty (.xml) 
 - `/simulations/` pre-computed SMETANA simulations (.tsv)
 - `/data/` various metadata, taxonomic assignments, media files, etc.
 - `/scripts/` markdown, r-markdown, and jupyter notebooks for each exercise
 - `/plots/` visualization of results 

## ☑️ Exercises
 0. [Start by cloning this repo](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/0.clone_repo.md)

### Part I
 1. [Use CarveMe to generate GEMs for a bacterial community](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/1.carve_models.md)
 2. [Visualize model metrics different species across species (modify to make summary of models for single communities)](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/2.plot_gut_model_summary.ipynb)
 3. [Use SMETANA detailed algorithm to predict metabolic interactions between species](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/3.run_smetana_detailed_interactions.md)
 4. [Visualize deteailed interactions with alluvial diagrams](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/4.plot_smetana_detailed_interactions.md)

### Part II
 5. [Use SMETANA global algorithm to generate MIP & MRO metrics for community of GEMs](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/5.run_smetana_global_metrics.md)
 6. [Visualize communities on cooperation-competition plot](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/6.plot_competition_cooperation.ipynb)
 7. [Generate ensemble models (optional)](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/7.generate_ensemble_models.md)
 8. [Quantify network uncertainity (optional)](https://github.com/franciscozorrilla/SymbNET/blob/main/scripts/8.plot_ensemble_dist.ipynb)

## 🍬 Tools

| Tool | Task | GitHub | Reference |
| :---         | :---           | :---          |  :---         | 
| CarveMe   | Build GEMs from MAGs   |[Repo](https://github.com/cdanielmachado/carveme)    |        [Paper](https://academic.oup.com/nar/article/46/15/7542/5042022)       |
| SMETANA     | Predict metabolic interactions between GEMs       | [Repo](https://github.com/cdanielmachado/smetana)      |          [Paper](https://www.pnas.org/content/112/20/6449)     |
| metaGEM   | Wrap tools & visualize results  | [Repo](https://github.com/franciscozorrilla/metaGEM)    | [Paper](https://academic.oup.com/nar/article/49/21/e126/6382386)    |
| Snakemake   | Workflow management and reproducibility    | [Repo](https://github.com/snakemake/snakemake)    | [Paper](https://f1000research.com/articles/10-33)   |

Pictured below is the metaGEM workflow for reconstructing and simulating metagenome based metabolic models. This training module will focus on how to generate and simulate communities of metabolic models using CarveMe and SMETANA.

<img align="center" src="https://github.com/franciscozorrilla/SymbNET/blob/main/plots/metaGEM/metagem_fig1.png" height = 600 width = 800>

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

## 🥃 Daniel's repos

### Tools

 - [DesignMC](https://github.com/cdanielmachado/designmc): Design microbial communities for production of specific target compounds using GEMs 

 - [HiOrCo](https://github.com/cdanielmachado/HiOrCo): Compute higher order cooccurence using abundance across samples

 - [Reframed](https://github.com/cdanielmachado/reframed): Metabolic modeling package

### Resources

 - [Cooccurrence paper](https://github.com/cdanielmachado/cooccurrence): Supplement repo to cooccurrence paper

 - [CarveMe paper](https://github.com/cdanielmachado/carveme_paper): Supplement repo to CarveMe paper

 - [Kefir paper](https://github.com/cdanielmachado/kefir_paper): Supplement repo to kefir paper

 - [EMBL GEMs](https://github.com/cdanielmachado/embl_gems): Collection of RefSeq-based GEMs

Please cite [Daniel Machado](https://orcid.org/0000-0002-2063-5383)'s relevant literature if you make use of these tools and/or resources.

## 📚 Suggested Reading

 - Intro to FBA: [What is flux balance analysis?](https://www.nature.com/articles/nbt.1614)
 - CarveMe: [Fast automated reconstruction of genome-scale metabolic models for microbial species and communities](https://academic.oup.com/nar/article/46/15/7542/5042022)
 - SMETANA: [Metabolic dependencies drive species co-occurrence in diverse microbial communities](https://www.pnas.org/content/112/20/6449)
 - metaGEM: [Reconstruction of genome scale metabolic models directly from metagenomes](https://academic.oup.com/nar/article/49/21/e126/6382386)
 - https://www.nature.com/articles/s41564-018-0123-9

## 🇪🇺 About SymbNET

SymbNET is a European network for host-microbe interactions research, funded by the European Union’s Horizon 2020 research and innovation programme. The project coordinated by FCG-IGC (Instituto Gulbenkian de Ciência, Portugal), brings together the world-leading research institutions EMBL (European Molecular Biology Laboratory, Germany),  CAU (Christian-Albrechts-Universität zu Kiel, Germany),  and UNIL (Université de Lausanne,  Switzerland), and a local widening partner ITQB NOVA (Instituto de Tecnologia Química e Biológica, Portugal).

This project has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement Nº 952537