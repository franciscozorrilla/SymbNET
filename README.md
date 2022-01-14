# 💻 SymbNET 🧬 From Metagenomics to Metabolic Interactions (Day 5) 

### 💰 Learning Outcomes

This module will cover practical aspects of metagenomics-based metabolic modeling:

 - Generating genome-scale metabolic models (GEMs) from metagenome assembled genomes (MAGs)
 - Predicting metabolic interactions within communities of GEMs
 - Exploring uncertainty in GEM reconstruction and simulation
 - Reference genomes vs MAGs/SAGs

### 🍬 Tools

| Tool | Task | GitHub | Reference |
| :---         | :---           | :---          |  :---         | 
| CarveMe   | Build GEMs from MAGs   |[Repo](https://github.com/cdanielmachado/carveme)    |        [Paper](https://academic.oup.com/nar/article/46/15/7542/5042022)       |
| SMETANA     | Predict metabolic interactions between GEMs       | [Repo](https://github.com/cdanielmachado/smetana)      |          [Paper](https://www.pnas.org/content/112/20/6449)     |
| metaGEM   | Wrap tools & visualize results  | [Repo](https://github.com/franciscozorrilla/metaGEM)    | [Paper](https://academic.oup.com/nar/article/49/21/e126/6382386)    |
| Snakemake   | Workflow management and reproducibility    | [Repo](https://github.com/snakemake/snakemake)    | [Paper](https://f1000research.com/articles/10-33)   |

The following figure shows the metaGEM workflow for reconstruction of MAGs and metabolic modeling. By now you will be familiar with the tools used for MAG generation, next you will learn how to generate and simulate communities of metabolic models using CarveMe and SMETANA.

![](https://github.com/franciscozorrilla/SymbNET/blob/main/plots/metaGEM/metagem_fig1.png)

### ⛏️ Datasets

The following table describes in detail the 6 small bacterial communities of 5 species that we will consider for metabolic modeling. These include MAG,SAG, and reference genome-based communities; the samples also span the human gut, kefir, and soil habitats.

| Microbiome |Genome type| Condition | Species | Links |
| :---        | :--- | :---           | :---          |  :---         | 
| Human gut  | MAGs |Normal Glucose Tolerance (NGT, ERR260255) |  <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>   | <ul><li>[Paper](https://www.nature.com/articles/nature12198)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/analyses/MGYA00001287#overview)</li></ul> |
| Human gut   | MAGs |Impaired Glucose Tolerance (IGT, ERR260172)      | <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>   |  <ul><li>[Paper](https://www.nature.com/articles/nature12198)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/analyses/MGYA00001094?version=1.0#overview)</li></ul> |
| Human gut  | MAGs | Type II Diabetes (T2D, ERR260140)  | <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>  | <ul><li>[Paper](https://www.nature.com/articles/nature12198)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/analyses/MGYA00001062?version=1.0#overview)</li></ul> |
| Human gut| Reference genomes | Reference genomes taken from RefSeq   | <ul><li>*B. uniformis*</li><li>*R. bromii*</li><li>*B. wexlerae*</li><li>*E. rectale*</li><li>*F. saccharivorans*</li></ul>  | <ul><li>[NCBI](https://www.ncbi.nlm.nih.gov/)</li></ul>   |
| Kefir | SAGs | Fermented with German grains (GER6)    | <ul><li>*L. mesenteroides*</li><li>*L. lactis*</li><li>*A. fabarum*</li><li>*L. kefiranofaciens*</li><li>*L. kefiri*</li></ul>  | <ul><li>[Paper](https://www.nature.com/articles/s41564-020-00816-5)</li></ul>   |
| Soil | MAGs |  Calcarosols from Uluru, Australia (ERR671933)   | <ul><li>f_Thermoleophilaceae</li><li>f_Herpetosiphonaceae</li><li>f_Phormidiaceae</li><li>f_Geodermatophilaceae</li><li>f_Rubrobacteraceae</li></ul>   | <ul><li>[Paper](https://academic.oup.com/gigascience/article/5/1/s13742-016-0126-5/2720982)</li><li>[metaGEM](https://github.com/franciscozorrilla/metaGEM_paper)</li><li>[MGnify](https://www.ebi.ac.uk/metagenomics/studies/MGYS00000434)</li></ul>  |


### 💡 Key points: CarveMe

1. The top-down approach
   - based on a universal and well-curated bacterial model, **carves** out a species specific model based on organism's genome.
2. The BiGG database
   - connects protein sequences with standardized and curated metabolic reaction knowledgebase.
3. The carving algorithm
   - MILP formulation to maximize presence of high genomic evidence reactions, minimize presence of low genomic evidence reactions, enforce gapless pathways.
4. The gap-filling algorithm
   - Uses genomic evidence scores to prioritize and minimize the number of added reactions needed to support growth on a given a media composition.

Kefir GEMs:
```
while read model;do 
   carve -v --mediadb data/milk_composition.tsv -g MILK --cobra -o ${model}.xml $model;
done< <(ls genomes/kefir/*.faa)
```

Gut GEMs:
```
while read model;do     
   carve -v --mediadb data/media_db.tsv -g M8 --cobra -o ${model}.xml $model;
done< <(ls genomes/gut_*.faa)
```

Soil GEMs:
```
while read model;do     
   carve -v --cobra -o ${model}.xml $model;
done< <(ls genomes/soil/*.faa)
```

Note: model carving and gapfilling problems can result in multiple possible solutions!

Use the ensemble flag to generate a user-defined number of equally plausible models to be stored in a single sbml file, e.g. `-n 100`. One can then calculate the pairwise jaccard distance between models within ensembles to [quantify network uncertainity](https://github.com/cdanielmachado/carveme_paper/blob/master/notebooks/Ensemble%20distances.ipynb).

Build ensemble models:
```
while read model;
 do carve -v --cobra -n 100 -o ${model}.xml $model; 
done< <(ls genomes/*.faa)
```

### 🔑 Key points: SMETANA

**Detailed algorithm**

1. The species coupling score (SCS) measures the dependence of growth of species A on species B (SCS<sub>A,B</sub>)
   - calculated by enumerating all possible community member subsets where species A can grow, SCS<sub>A,B</sub> is the fraction of subsets where both species A and B can grow.
2. The metabolite uptake score (MUS) measures the dependence of growth of species A on metabolite *m* (MUS<sub>A,*m*</sub>)
   - calculated by enumerating all possible metabolite requirement subsets where species A can grow, MUS<sub>A,*m*</sub> is the fraction of subsets where both species A grows and metabolite *m* is taken up.
3. The metabolite production score (MPS) is a binary score indicating whether a given species B can produce metabolite *m* (MPS = 1) or not (MPS = 0) in the community of N members (MPS<sub>B,*m*</sub>)
4. The SMETANA score ranges from 0 to 1
   - measures how strongly a receiver species relies on a donor species for a particular metabolite
   - SMETANA<sub>A,B,*m*</sub> = SCS<sub>A,B</sub> * MUS<sub>A,*m*</sub> * MPS<sub>B,*m*</sub>

Note: There may be equivalent solutions that satisfy the linear programming problems posed by the detailed algorithm. To explore the solution space run multiple simulations and then take averages.

Gut example:
```
smetana --flavor cobra -o gut_normal -v -d --mediadb data/media_db.tsv -m M3 *.xml
```

Soil example:
```
for i in {1..100}; do 
 echo "Running simulation $i out of 100 ... "; 
 smetana --flavor ucsd -o sim_${i} -v -d --molweight --zeros *.xml;
done
```

**Global algorithm**

1. The metabolic interaction potential (MIP) measures the propensity of a given community to exchange metabolites, and is defined as the maximum number of essential nutritional components that a community can provide for itself through interspecies metabolic exchanges.
2. The metabolic resource overlap (MRO) measures the degree of metabolic competition in a community, and is defined as the maximum possible overlap between the minimal nutritional requirements of all member species.

Note: Use `--cobra` flag in CarveMe run and `--flavor ucsd` in SMETANA run to calculate global parameters MIP and MRO (metabolic resource overlap).

```
for i in {1..100}; do 
 echo "Running simulation $i out of 100 ... "; 
 smetana --flavor ucsd -o sim_${i} -v -g *.xml;
done

```

### 🕺 Daniel's repos

**Tools**

 - [DesignMC](https://github.com/cdanielmachado/designmc): Design microbial communities for production of specific target compounds using GEMs 

 - [HiOrCo](https://github.com/cdanielmachado/HiOrCo): Compute higher order cooccurence using abundance across samples

 - [Reframed](https://github.com/cdanielmachado/reframed): Metabolic modeling package

**Resources**

 - [Cooccurrence paper](https://github.com/cdanielmachado/cooccurrence): Supplement repo to cooccurrence paper

 - [CarveMe paper](https://github.com/cdanielmachado/carveme_paper): Supplement repo to CarveMe paper

 - [Kefir paper](https://github.com/cdanielmachado/kefir_paper): Supplement repo to kefir paper

 - [EMBL GEMs](https://github.com/cdanielmachado/embl_gems): Collection of RefSeq-based GEMs

Please cite [Daniel Machado](https://orcid.org/0000-0002-2063-5383)'s relevant literature if you make use of these tools and resources!

### 📚 Suggested Reading

 - Intro to FBA: [What is flux balance analysis?](https://www.nature.com/articles/nbt.1614)
 - CarveMe: [Fast automated reconstruction of genome-scale metabolic models for microbial species and communities](https://academic.oup.com/nar/article/46/15/7542/5042022)
 - SMETANA: [Metabolic dependencies drive species co-occurrence in diverse microbial communities](https://www.pnas.org/content/112/20/6449)
 - metaGEM: [Reconstruction of genome scale metabolic models directly from metagenomes](https://academic.oup.com/nar/article/49/21/e126/6382386)
 - https://www.nature.com/articles/s41564-018-0123-9

### 🇪🇺 About SymbNET

SymbNET is a European network for host-microbe interactions research, funded by the European Union’s Horizon 2020 research and innovation programme. The project coordinated by FCG-IGC (Instituto Gulbenkian de Ciência, Portugal), brings together the world-leading research institutions EMBL (European Molecular Biology Laboratory, Germany),  CAU (Christian-Albrechts-Universität zu Kiel, Germany),  and UNIL (Université de Lausanne,  Switzerland), and a local widening partner ITQB NOVA (Instituto de Tecnologia Química e Biológica, Portugal).

This project has received funding from the European Union’s Horizon 2020 research and innovation programme under grant agreement Nº 952537
