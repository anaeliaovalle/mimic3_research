# mimic3 project

MIMIC3 Project.ipynb contains tables pertaining to Thrombocytopenia / Heparin-Induced Thrombocytopenia Patients such as:
- [Admissions and Demographics](https://mimic.physionet.org/mimictables/admissions/) (3,524 rec)
- [Chart events](https://mimic.physionet.org/mimictables/chartevents/) (>1000 rec)   
- [Patient notes](https://mimic.physionet.org/mimictables/noteevents/) (8,088 rec)
- [Patient procedures](https://mimic.physionet.org/mimictables/procedureevents_mv/) (12,802 rec)
- [Microbiology events](https://mimic.physionet.org/mimictables/microbiologyevents/) (10,636 rec)
- [Lab events](https://mimic.physionet.org/mimictables/labevents/) (17 rec)
- [Heparin use](https://mimic.physionet.org/mimictables/prescriptions/)(123,064 rec)
- [Argatroban use](https://mimic.physionet.org/mimictables/prescriptions/) (768 rec)
- [Steroid use](https://mimic.physionet.org/mimictables/prescriptions/) (69,567 rec)

The csv files provide the first 6 tables in csv format. All tables correspond to patients with HIT or Thrombocytopenia unless otherwise stated. Documentation for each table can be found by clicking on the table link. 

### Steroid vs Non-Steroid Use with Heparin-Induced Thrombocytopenia Patients: 
- yes_steroid.csv (25 records)
- no_steroid.csv (64 records)

##### Discrepancies 
- [p_labs.csv]Presence of positive Pf4 antibody test OR HIT positive serology
    - p_labs.csv provides the HIT/thrombo patients that have had blood tests labeled 'heparin' or 'heparin,LMW'. This may or may not be the same types of tests
- [NOT FOUND]Positive serotonin release assay
- [NOT FOUND] Platelet count < 150,000
- Many tables are sparse in data with either little records or incomplete rows
