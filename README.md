# CS109A_Project
Final project for Harvard CS109A 2017

### Data 
Raw data downloaded from Census:
- /data/census/raw/

Processed 2010 data for EDA:
- /data/merged/eda_2010.pkl
- /data/merged/eda_2010.csv

### Scripts
Script to load and process 2010 data to EDA ready format:
- scripts/load_and_process_data.ipynb

> Once EDA is completed the full processing of all datasets must be done.

> Only subset of features will be considered and only those that exist in all datasets.

#### Issues Encountred:
- various years of FBI data has different url format and table tags
- various years of Census data has different metadata for columns, therefore simple merging is complicated.
- Census data is also in follows different formats and file naming conventions
- FBI data contained many more MSAs (~300 vs 100) than in Census data
