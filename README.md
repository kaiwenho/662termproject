# A Novel Natural Language Processing Technique for Preventing Loss of Term Specificity in the National Clinical Trial Database
Kaiwen He & Michael Patton
University of Alabama at Birmingham


The National Clinical Trial (NCT) database represents a wealth of information (> 160,000 trials, Phase 1-4) for medical providers and patients alike; however, accessing this data is notoriously difficult. While previous efforts to parse the NCT have increased accessibility to valuable content; use of the Medical Subject Heading (MeSH) ontology alone results in loss of term specificity for descriptions of trial interventions and diseases.

We used CubNer (Zhang & Elhadad, 2013) to locate the disease and intervention mentions on the NCT free-text descriptions. The output of CubNer is string matched against custom vocabularies derived from the Observational Medical Outcomes Partnership (OMOP) ontology. DNorm (Leaman, Doğan & Lu, 2013) is also applied with the NCT free-text descriptions, and the returned structured identifiers are map to the names.

Improvements for Disease Recognition in NCT Descriptions

  - 46,049 total Clinical Trials gained 1 or more structured identifiers (avg 1.62 new identifiers per trial)

  - 15,625 Clinical Trials with no corresponding MeSH term for disease description were annotated with 1 or more structured identifiers

Improvements for Intervention Recognition in NCT Descriptions

  - 21,405 total Clinical Trials gained 1 or more structured identifiers (avg 1.47 new identifiers per trial)

  - 19,091 Clinical Trials with no corresponding MeSH term for intervention description were annotated with 1 or more structured identifiers
