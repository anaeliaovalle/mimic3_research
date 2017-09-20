### Steroid vs Non-Steroid Use with Heparin-Induced Thrombocytopenia Patients:

The 2 tables are split up between HIT patients with steroid use (25 rec) and non-steroid use (64 rec).

#### Features:
- **subject_id**: Patient id: Unique INT
- **hadm_id**: Hospital admission id : Unique INT
  - One subject may have more than one hadm_id, indicating multiple admissions
- **gender**: Gender of patient (M or F): String
- **dob**: Date of birth : Date
- **first_admit_age**: age at first admittance: INT
  - To protect patient information, age is not given. To derive this, we must take first admit date - patient dob. Any patient > 89 has an age of 300. Therefore, we only have actual ages from people younger than 89.
- **first_admittime**: Timestamp of patient's first admittance to hospital: Date
- **admittime**: Timestamp of patient's admittance to hospital or clinic: Date
- **dischtime**: Timestamp of patient's discharge from hospital or clinic: Date
- **duration**: Duration of stay: INT
  - This is taken from subtracting dischtime from admittime
- **age_group**: Age group of patient: String
- **deathtime**: Timestamp of patient death : Date
- **admission_type**: Describes the type of admission: String
- **diagnosis**: Diagnosis of patient: String
  - This is a preliminary, free text diagnosis for the patient on hospital admission. The diagnosis is usually assigned by the admitting clinician and does not use a systematic ontology.
  - **NOTE** The final diagnosis for all patients is Heparin-Induced Thrombocytopenia
- **mortality_bin**: Flag describing whether or not the patient passed away (1 or 0): INT
- **bleeding_bin**: Flag describing whether or not the patient had any bleeding issues throughout their admission (1 or 0): INT
  - This was created by searching through all chart notes for a subject_id/hadm_id. If the keyword 'bleeding' was found exclusively or as part of a word within their chart, it was added a running count of occurences. If occurences > 0, then 1 for bleeding_bin.

More information on features can be found in tables used in the SQL code and cross referencing them [here](https://mimic.physionet.org/mimictables/admissions/).

#### Methodology
It was found that multiple HIT patients have several admission times where they may or may not have used steroids as treatment. To get a clean separation between use/not use, the following steps were taken:
1) A table was created that had all patient data (filtered by the icd9 code that is HIT dx), those that used steroids (e.g. prednisone, methylprednisolone, or dexamethasone) and those that did not use steroids.
2) We then get the earliest timestamp of admission for ALL of the patients in step 1 in order to get one subject_id/hadm_id
that provided the earliest diagnosis.
3) It was seen that even though we had a unique subject_id/hadm_id, there were several drugs each patient took at a given admission date. To separate those that took versus didn't take steroids, all drug names that were steroid names were counted for that particular patient/admission. If the count of the occurrence > 0, then they must belong to the steroid use group. Vice versa, if count < 1, then the patient did not take steroids at any time during that admission.
4) Each patient's chart notes are then searched for keywords like 'bleeding' to get a count of thrombolytic events. If the count is greater than 1, they experienced bleeding, else they did not.
5) Each group has its own table is joined with relevant demographic data, then outputted to csv.
