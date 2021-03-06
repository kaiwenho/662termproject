# A Novel Natural Language Processing Technique for Preventing Loss of Term Specificity in the National Clinical Trial Database
Kaiwen He & Michael Patton

University of Alabama at Birmingham


The National Clinical Trial (NCT) database represents a wealth of information (> 160,000 trials, Phase 1-4) for medical providers and patients alike; however, accessing this data is notoriously difficult. While previous efforts to parse the NCT have increased accessibility to valuable content; use of the Medical Subject Heading (MeSH) ontology alone results in loss of term specificity for descriptions of trial interventions and diseases

Using an integrated free text processing approach (CubNER (Zhang & Elhadad, 2013) + DNorm (Leaman, Doğan & Lu, 2013)), combined string matching and concept synonymization with Observational Medical Outcomes Partnership (OMOP) ontology, we aim to improve coverage of diseases and interventions described in NCTs.

Improvements for Disease Recognition in NCT Descriptions

- 66,067 total Clinical Trials gained 1 or more structured identifiers (avg 1.40 new identifiers per trial)
- 31,497 Clinical Trials with no corresponding MeSH term for disease description were annotated with 1 or more structured identifiers
- Concept synonymization of new disease annotations produced an average of 2.30 synonyms per NCT entry


Improvements for Intervention Recognition in NCT Descriptions

- 84,490 total Clinical Trials gained 1 or more structured identifiers (avg 1.32 new identifiers per trial)
- 59,383 Clinical Trials with no corresponding MeSH term for intervention description were annotated with 1 or more structured identifiers
- Concept synonymization of new intervention annotations produced an average of 6.43 synonyms per NCT entry


### Datasets
The dataset, including the original data and the preprocessed data, can be downloaded from https://drive.google.com/file/d/1xAZhkLFo6T4fb_2W2Ii-3fDX3yOo4kwS/view?usp=sharing. The data file should be in the same directory of the Jupyter notebooks (Treatment_entity_extraction.ipynb and clean_data_and_reformat.ipynb). The README.txt contains the description for each data file.

Files for building the OMOP ontology prior to running omop_ontology_builder_with_stats_for_nlp.rmd can be downloaded from https://drive.google.com/drive/folders/1iF8yZMv_PwmqSAYdQ3ADouxLdPHccL6L?usp=sharing. The data files, along with the Jupyter notebook data, should be in the same director as the .rmd file prior to running the script. 

### Run the data in CubNER
The official website of CubNER is https://people.dbmi.columbia.edu/~szhang/ner.html. You may download the source code and setup CubNER in your PC by following its README.txt file.

To repeat the result of this project, firstly, comment out the test class in domain_rep_sample.xml. Next, move the treatment_description_only.txt from data directory to the directory of CubNER. Then run the command line

  `java -jar CubNER.jar seed -c domain_rep_sample.xml`

to build the seed terms. Lastly, run

  `java -jar CubNER.jar recognize -b treatment_description_only.txt -f treatment_description_only.txt`

to do the NER tagging. The tagged tokens will be in a file called treatment_description_only.txt_tagged. It takes about 3 hours to finish running. You may separate the disease and intervention tagging by using just one class of seed term in domain_rep_sample.xml. Every time you update the seed term, you should delete the old seed file and rerun `java -jar CubNER.jar seed -c domain_rep_sample.xml`.

### Run the data in DNorm
You may download the source code of DNorm from https://www.ncbi.nlm.nih.gov/research/bionlp/Tools/ (scroll down to Software) and setup DNorm by following its README.txt file.

Before running any command line, please move the file PubTator_cleaned_des.tsv from data directory to the DNorm directory. Then run the command line

  `./ApplyDNorm.sh config/banner_NCBIDisease_UMLS2013AA_TEST.xml data/CTD_diseases.tsv output/simmatrix_NCBIDisease_e4.bin AB3P_DIR TEMP PubTator_cleaned_des.tsv PubTator_cleaned_des_out.txt`

The returned file is called PubTator_cleaned_des_out.txt in the DNorm directory after the above command line finishing running. 

### Run OMOP ontology builder and evaluate statistics of CubNER and DNorm output on NCT database files
To run omop_ontology_builder_with_stats_for_nlp.rmd, either download R version > 4.0 and run at the command line or load Rstudio and run the file following the instructions outlined Datasets. The script will build an concept normalization path using the OMOP datafiles and string match the output of CubNER and DNorm to structured vocabularies within OMOP. Next the script will print statistics for number of NCT trials without annotations that have been populated as a result of the CubNER and DNorm processing. Additionally, the script will show the number of new synonyms per NCT trial added as a result of the Cubner and DNorm processing. 
