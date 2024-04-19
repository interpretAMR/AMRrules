# Interpretive standards for AMR genotypes

Organism-specific interpretation of antimicrobial susceptibility testing (AST) data is standard in clinical microbiology, with rules regularly reviewed by expert committees of [CLSI](https://clsi.org/) and [EUCAST](https://www.eucast.org/). EUCAST also maintains lists of [expert rules](https://www.eucast.org/expert_rules_and_expected_phenotypes) for some species, including [expected (intrinsic) resistance](https://www.eucast.org/expert_rules_and_expected_phenotypes/expected_phenotypes) and expected susceptibility phenotypes, to guide clinical labs in deciding which drugs to test and whether/how to report them.

We propose there is a similar need for systematic rules for the organism-specific interpretation of antimicrobial resistance (AMR) genotypes derived from pathogen whole genome sequence (WGS) data.

Current solutions focus on bespoke solutions for specific organisms (e.g. our [Kleborate](https://github.com/klebgenomics/Kleborate) tool for _Klebsiella pneumoniae_; Pathogenwatch [AMR libraries](https://gitlab.com/cgps/pathogenwatch/amr-libraries) for [_Salmonella_ Typhi](https://doi.org/10.1038/s41467-021-23091-2), [_Neisseria gonorrhoeae_](https://doi.org/10.1186/s13073-021-00858-2) and others; [Resfinder 4.0](https://bitbucket.org/genomicepidemiology/resfinder_db/src/master/) for _E. coli_ and others; [Mykrobe](https://github.com/Mykrobe-tools/mykrobe) and [TBProfiler](https://github.com/jodyphelan/TBProfiler) tools for _Mycobacterium tuberculosis_), but this complicates bioinformatics analyses and promotes fragmentation rather than consolidation of expertise. [AbritAMR](https://github.com/MDU-PHL/abritamr) offers a potential solution for multiple organisms, but organism-specific interpretation rules are hard-coded in Python and separated from supporting evidence, making the logic difficult for others to curate and update.

This repo outlines a proposal for a simple data structure to store organism-specific rules for the interpretation of AMR genotype data, that could be used to enrich the outputs of standard AMR genotyping tools (such as AMRfinderplus and other tools, with or without [hAMRonization](https://github.com/pha4ge/hAMRonization)) and generate informative genome reports that capture expert knowledge about how core genes contribute to antimicrobial susceptibility.

Example rules are given for _Klebsiella pneumoniae_, and [example code](https://github.com/interpretAMR/AMRrules/blob/main/parse_amrfinder.py) is given to annotate NCBI [AMRfinderplus](https://www.ncbi.nlm.nih.gov/pathogens/antimicrobial-resistance/AMRFinder/) results for _Klebsiella pneumoniae_ using these rules.

The rule specification (still a work in progress) is available in [this Google sheet](https://docs.google.com/spreadsheets/d/1N0HXK8T5EH-4XDonvW5RmAm8tJTb1RlIMB1oF2x4ss8/edit?usp=sharing) (guidance on tab 2).


## Data analysis pipeline
![pipeline_image](pipeline.png?raw=true)

## Organism-specific rules
![rules_table](organism_specific_rules.png?raw=true)

Example file: [organism_specific_rules.tsv](organism_specific_rules.tsv)

## Annotated gene table
![annotated_gene_report](annotated_gene_report.png?raw=true)

Example file: [annotated_gene_report.tsv](annotated_gene_report.tsv)

### Example code

This file can be generated by annotating AMRfinder plus output with the above organism-specific rules for _Klebsiella pneumoniae_, using [parse_amrfinder.py](parse_amrfinder.py):

```
./parse_amrfinder.py --reports example_data_kleb/*_amrFinderPlusOutput.tsv 
                     --species 'Klebsiella pneumoniae'
                     --organism_rules organism_specific_rules.tsv
                     --drug_dictionary example_dict_kleb/Kleb_local_dict.tsv
                     --output example_annotatedAMRreport.tsv
```

## Genome report
![genome_report](genome_report.png?raw=true)

Example file (PDF): [genome_report.pdf](genome_report.pdf)

Example file (RTF): [genome_report.rtf](genome_report.rtf)

## Contributors
This concept was workshopped by members of the [Holt lab](https://holtlab.net) at [London School of Hygiene and Tropical Medicine](https://www.lshtm.ac.uk) and further developed in collaboration with [Jane Hawkey](https://github.com/jhawkey) at [Monash University](https://research.monash.edu/en/persons/jane-hawkey).
