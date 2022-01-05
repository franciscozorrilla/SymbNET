# 💻 SymbNET 🧬

## 🔬 From Metagenomics to Metabolic Interactions (Day 5)

### 💰 Learning Outcomes

This module will cover practical aspects of metagenomics-based metabolic modeling:

 - Generating genome-scale metabolic models (GEMs) from metagenome assembled genomes (MAGs)
 - Predicting metabolic interactions within communities of GEMs
 - Visualizing the effect of gapfilling and simulation media
 - Exploring the panmetabolism of conspecifc genomes

### 🍬 Tools

| Tool | Task | GitHub | Reference |
| :---         | :---           | :---          |  :---         | 
| CarveMe   | Build GEMs from MAGs   |[Repo](https://github.com/cdanielmachado/carveme)    |        [Paper](https://academic.oup.com/nar/article/46/15/7542/5042022)       |
| SMETANA     | Predict metabolic interactions between GEMs       | [Repo](https://github.com/cdanielmachado/smetana)      |          [Paper](https://www.pnas.org/content/112/20/6449)     |
| metaGEM   | Wrap tools & visualize results  | [Repo](https://github.com/franciscozorrilla/metaGEM)    | [Paper](https://academic.oup.com/nar/article/49/21/e126/6382386)    |
| Snakemake   | Workflow management and reproducibility    | [Repo](https://github.com/snakemake/snakemake)    | [Paper](https://f1000research.com/articles/10-33)   |

### 💡 Understanding CarveMe

1. The top-down approach: create one universal well-curated bacterial model, **carve** out a species specific model based on organism's genome.
2. The BiGG database: connects protein sequences with standardized and curated metabolic reaction knowledgebase.
3. The carving algorithm: MILP problem to maximize presence of high genomic evidence reactions, minimize presence of low genomic evidence reactions, enforce gapless pathways.
4. The gap-filling algorithm: Uses genomic evidence scores to minimize the number of added reactions needed to support growth on a given a media composition.

Note: model carving and gapfilling problems can result in multiple possible solutions!

### 🍱 Tentative structure

- Carve your own MAGs
  - Dump MAGs into folder, run Snakefile rule to carve in series or in parallel
  - Run model_vis.R script to visualize rxns,speices,number genes
  - Classify GEMs/MAGs using metaGEM-gtdbtk (if not done previously)
- Run most basic SMETANA example with 2 species
  - Could have them use metaGEM parser for this and previous step
  - Run smetana_vis.R script to visualize interactions in one medium
  - Change media composition with basic 2 species example
  - Run smetana_vis.R to visualize differences in interactions across 2 different media
- Choose your own adventure, explore either:
  - Interactions across 10 different media for 2 species
  - Interactions across 2 different media for 5 species
- Real world test case: metaGEM gut dataset
  - Go through dataset and analysis, showing how different mets/donors/receivers were identified across conditions
  - Simulate interactions between X species across all samples where species are present, identify statistically significant differences, visualize results
- Discussion on different analysis options/avenues
  - Other applications?
 
### 📚 Suggested Reading

 - Intro to FBA: [What is flux balance analysis?](https://www.nature.com/articles/nbt.1614)
 - CarveMe: [Fast automated reconstruction of genome-scale metabolic models for microbial species and communities](https://academic.oup.com/nar/article/46/15/7542/5042022)
 - SMETANA: [Metabolic dependencies drive species co-occurrence in diverse microbial communities](https://www.pnas.org/content/112/20/6449)
 - metaGEM: [Reconstruction of genome scale metabolic models directly from metagenomes](https://academic.oup.com/nar/article/49/21/e126/6382386)

### 🇪🇺 About SymbNET

SymbNET is a European network for host-microbe interactions research, funded by the European Union’s Horizon 2020 research and innovation programme. The project coordinated by FCG-IGC (Instituto Gulbenkian de Ciência, Portugal), brings together the world-leading research institutions EMBL (European Molecular Biology Laboratory, Germany),  CAU (Christian-Albrechts-Universität zu Kiel, Germany),  and UNIL (Université de Lausanne,  Switzerland), and a local widening partner ITQB NOVA (Instituto de Tecnologia Química e Biológica, Portugal).

This project has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement Nº 952537
