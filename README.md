# 💻 SymbNET 🧬 From Metagenomics to Metabolic Interactions (Day 5) 

## 💰 Learning Outcomes

 - Generating genome-scale metabolic models (GEMs) from metagenome assembled genomes (MAGs)
 - Predicting metabolic interactions within communities of GEMs
 - Exploring uncertainty in GEM reconstruction and simulation
 - Reference genomes vs MAGs/SAGs

## ☑️ Exercises

 1. Use CarveMe to generate a community of GEMs
 2. Visualize model metrics different species across conditions
 3. Generate ensemble models
 4. Quantify network uncertainity
 5. Use SMETANA global algorithm to generate MIP & MRO metrics for community of GEMs
 6. Visualize communities on cooperation-competition plot
 7. Use SMETANA detailed algorithm to predict metabolic interactions between species
 8. Visualize deteailed interactions with alluvial diagrams

## 🍬 Tools

| Tool | Task | GitHub | Reference |
| :---         | :---           | :---          |  :---         | 
| CarveMe   | Build GEMs from MAGs   |[Repo](https://github.com/cdanielmachado/carveme)    |        [Paper](https://academic.oup.com/nar/article/46/15/7542/5042022)       |
| SMETANA     | Predict metabolic interactions between GEMs       | [Repo](https://github.com/cdanielmachado/smetana)      |          [Paper](https://www.pnas.org/content/112/20/6449)     |
| metaGEM   | Wrap tools & visualize results  | [Repo](https://github.com/franciscozorrilla/metaGEM)    | [Paper](https://academic.oup.com/nar/article/49/21/e126/6382386)    |
| Snakemake   | Workflow management and reproducibility    | [Repo](https://github.com/snakemake/snakemake)    | [Paper](https://f1000research.com/articles/10-33)   |

The following figure shows the metaGEM workflow for reconstruction of MAGs and metabolic modeling. By now you will be familiar with the tools used for MAG generation, next you will learn how to generate and simulate communities of metabolic models using CarveMe and SMETANA.

![](https://github.com/franciscozorrilla/SymbNET/blob/main/plots/metaGEM/metagem_fig1.png)

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


## 🪚 CarveMe

### Usage

```
$ carve -h

smusage: carve [-h] [--dna | --egg | --refseq] [--diamond-args DIAMOND_ARGS]
             [-r] [-o OUTPUT] [-u UNIVERSE | --universe-file UNIVERSE_FILE]
             [--cobra | --fbc2] [-n ENSEMBLE] [-g GAPFILL] [-i INIT]
             [--mediadb MEDIADB] [-v] [-d] [--soft SOFT] [--hard HARD]
             [--reference REFERENCE]
             INPUT [INPUT ...]

Reconstruct a metabolic model using CarveMe

positional arguments:
  INPUT                 Input (protein fasta file by default, see other options for details).
                        When used with -r an input pattern with wildcards can also be used.
                        When used with --refseq an NCBI RefSeq assembly accession is expected.

optional arguments:
  -h, --help            show this help message and exit
  --dna                 Build from DNA fasta file
  --egg                 Build from eggNOG-mapper output file
  --refseq              Download genome from NCBI RefSeq and build
  --diamond-args DIAMOND_ARGS
                        Additional arguments for running diamond
  -r, --recursive       Bulk reconstruction from folder with genome files
  -o OUTPUT, --output OUTPUT
                        SBML output file (or output folder if -r is used)
  -u UNIVERSE, --universe UNIVERSE
                        Pre-built universe model (default: bacteria)
  --universe-file UNIVERSE_FILE
                        Reaction universe file (SBML format)
  --cobra               Output SBML in old cobra format
  --fbc2                Output SBML in sbml-fbc2 format
  -n ENSEMBLE, --ensemble ENSEMBLE
                        Build model ensemble with N models
  -g GAPFILL, --gapfill GAPFILL
                        Gap fill model for given media
  -i INIT, --init INIT  Initialize model with given medium
  --mediadb MEDIADB     Media database file
  -v, --verbose         Switch to verbose mode
  -d, --debug           Debug mode: writes intermediate results into output files
  --soft SOFT           Soft constraints file
  --hard HARD           Hard constraints file
  --reference REFERENCE
                        Manually curated model of a close reference species.
```

### Key points

1. The top-down approach
   - based on a universal and well-curated bacterial model, **carves** out a species specific model based on organism's genome.
2. The BiGG database
   - connects protein sequences with standardized and curated metabolic reaction [knowledgebase](http://bigg.ucsd.edu/).
3. The carving algorithm
   - MILP formulation to maximize presence of high genomic evidence reactions, minimize presence of low genomic evidence reactions, enforce gapless pathways.
4. The gap-filling algorithm
   - Uses genomic evidence scores to prioritize and minimize the number of added reactions needed to support growth on a given a media composition.

### Example code

#### Kefir GEMs
```
while read model;do 
   carve -v --mediadb data/milk_composition.tsv -g MILK --cobra -o ${model}.xml $model;
done< <(ls genomes/kefir/*.faa)
```

#### Gut GEMs
```
while read model;do     
   carve -v --mediadb data/media_db.tsv -g M8 --cobra -o ${model}.xml $model;
done< <(ls genomes/gut_*.faa)
```

#### Soil GEMs
```
while read model;do     
   carve -v --cobra -o ${model}.xml $model;
done< <(ls genomes/soil/*.faa)
```

Note: the posed linear programming model carving and gapfilling problems can result in multiple equivalent solutions. Use the ensemble flag to generate a user-defined number of equally plausible models to be stored in a single sbml file, e.g. `-n 100`. One can then calculate the pairwise jaccard distance between models within ensembles to [quantify network uncertainity](https://github.com/cdanielmachado/carveme_paper/blob/master/notebooks/Ensemble%20distances.ipynb).

#### Build ensemble models
```
while read model;
 do carve -v --cobra -n 100 -o ${model}.xml $model; 
done< <(ls genomes/*.faa)
```

## 🔑 SMETANA

### Usage

```
$ smetana -h

usage: smetana [-h] [-c COMMUNITIES.TSV] [-o OUTPUT] [--flavor FLAVOR]
               [-m MEDIA] [--mediadb MEDIADB]
               [-g | -d | -a ABIOTIC | -b BIOTIC] [-p P] [-n N] [-v] [-z]
               [--solver SOLVER] [--molweight] [--exclude EXCLUDE]
               [--no-coupling]
               MODELS [MODELS ...]

Calculate SMETANA scores for one or multiple microbial communities.

positional arguments:
  MODELS                
                        Multiple single-species models (one or more files).
                        
                        You can use wild-cards, for example: models/*.xml, and optionally protect with quotes to avoid automatic bash
                        expansion (this will be faster for long lists): "models/*.xml". 

optional arguments:
  -h, --help            show this help message and exit
  -c COMMUNITIES.TSV, --communities COMMUNITIES.TSV
                        
                        Run SMETANA for multiple (sub)communities.
                        The communities must be specified in a two-column tab-separated file with community and organism identifiers.
                        The organism identifiers should match the file names in the SBML files (without extension).
                        
                        Example:
                            community1	organism1
                            community1	organism2
                            community2	organism1
                            community2	organism3
                        
  -o OUTPUT, --output OUTPUT
                        Prefix for output file(s).
  --flavor FLAVOR       Expected SBML flavor of the input files (cobra or fbc2).
  -m MEDIA, --media MEDIA
                        Run SMETANA for given media (comma-separated).
  --mediadb MEDIADB     Media database file
  -g, --global          Run global analysis with MIP/MRO (faster).
  -d, --detailed        Run detailed SMETANA analysis (slower).
  -a ABIOTIC, --abiotic ABIOTIC
                        Test abiotic perturbations with given list of compounds.
  -b BIOTIC, --biotic BIOTIC
                        Test biotic perturbations with given list of species.
  -p P                  Number of components to perturb simultaneously (default: 1).
  -n N                  
                        Number of random perturbation experiments per community (default: 1).
                        Selecting n = 0 will test all single species/compound perturbations exactly once.
  -v, --verbose         Switch to verbose mode
  -z, --zeros           Include entries with zero score.
  --solver SOLVER       Change default solver (current options: 'gurobi', 'cplex').
  --molweight           Use molecular weight minimization (recomended).
  --exclude EXCLUDE     List of compounds to exclude from calculations (e.g.: inorganic compounds).
  --no-coupling         Don't compute species coupling scores.
```

### Key points

#### Detailed algorithm

1. The species coupling score (SCS) measures the dependence of growth of species A on species B (SCS<sub>A,B</sub>)
   - calculated by enumerating all possible community member subsets where species A can grow, SCS<sub>A,B</sub> is the fraction of subsets where both species A and B can grow.
2. The metabolite uptake score (MUS) measures the dependence of growth of species A on metabolite *m* (MUS<sub>A,*m*</sub>)
   - calculated by enumerating all possible metabolite requirement subsets where species A can grow, MUS<sub>A,*m*</sub> is the fraction of subsets where both species A grows and metabolite *m* is taken up.
3. The metabolite production score (MPS) is a binary score indicating whether a given species B can produce metabolite *m* (MPS = 1) or not (MPS = 0) in the community of N members (MPS<sub>B,*m*</sub>)
4. The SMETANA score ranges from 0 to 1
   - measures how strongly a receiver species relies on a donor species for a particular metabolite
   - SMETANA<sub>A,B,*m*</sub> = SCS<sub>A,B</sub> * MUS<sub>A,*m*</sub> * MPS<sub>B,*m*</sub>

#### Global algorithm

1. The metabolic interaction potential (MIP) measures the propensity of a given community to exchange metabolites, and is defined as the maximum number of essential nutritional components that a community can provide for itself through interspecies metabolic exchanges.
2. The metabolic resource overlap (MRO) measures the degree of metabolic competition in a community, and is defined as the maximum possible overlap between the minimal nutritional requirements of all member species.


### Example code

Note: Use `--cobra` flag in CarveMe run and `--flavor ucsd` in SMETANA run to calculate global parameters MIP and MRO (metabolic resource overlap).

#### Running a series of global simulations
```
for i in {1..100}; do 
 echo "Running simulation $i out of 100 ... "; 
 smetana --flavor ucsd -o sim_${i} -v -g *.xml;
done
```

#### Gut example for detailed interactions
```
smetana --flavor cobra -o gut_normal -v -d --mediadb data/media_db.tsv -m M3 *.xml
```

Note: There may be equivalent solutions that satisfy the linear programming problems posed by the detailed and global algorithms. To explore the solution space run multiple simulations and then take averages. Use the `--molweight` flag to predict interactions on community-specific minimal media. Use the `--zeros` flag to take averages across samples.

#### Running a series of detailed simulations
```
for i in {1..100}; do 
 echo "Running simulation $i out of 100 ... "; 
 smetana --flavor ucsd -o sim_${i} -v -d --molweight --zeros *.xml;
done
```

## 🏖️ Daniel's repos

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
