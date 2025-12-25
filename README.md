# Predicting In-Hospital Cardiac Arrest in Sepsis Patients

## Overview

This repository contains a **data science research project** focused on predicting **in-hospital cardiac arrest among sepsis patients** using structured electronic health record (EHR) data from the MIMIC-III clinical database.

The project is framed as a **clinical risk prediction problem**, emphasizing cohort construction, data cleaning, exploratory analysis, and interpretable modeling. The goal is to assess whether patient demographics and admission-related features available early in a hospital stay contain a meaningful predictive signal for cardiac arrest risk.

---

## Research Question

**Can patient demographics and admission-related characteristics be used to predict in-hospital cardiac arrest among patients diagnosed with sepsis?**

---

## Key Findings

- **Age** is a strong predictor of in-hospital cardiac arrest among sepsis patients.
- **Emergency admissions** are associated with higher arrest risk compared to other admission types.
- Admission context and basic demographic features may serve as useful early indicators for clinical risk stratification.

These results suggest that relatively simple, early-available features can provide a meaningful signal for downstream predictive models.

---

## Data Source

- **MIMIC-III Clinical Database**
- De-identified ICU patient data from a single tertiary-care hospital
- Age values capped at 89 years to comply with HIPAA de-identification standards

Access to MIMIC-III requires credentialing and completion of required training.

---

## Methodology

### Phase II: Data Cleaning and Cohort Construction

Data preprocessing and cohort construction are performed in `01_data_cleaning.ipynb`, including:

- Filtering admissions to identify sepsis-related ICU stays
- Identifying in-hospital cardiac arrest outcomes
- Merging admissions, ICU stay, and transfer-level tables
- Cleaning demographic and admission-related variables

The resulting cleaned cohort is exported as a structured tabular dataset for downstream analysis.

### Exploratory Data Analysis

- Distributional analysis of age and admission types
- Examination of outcome prevalence across patient subgroups

### Modeling Approach

- Iterative, interpretable model development informed by exploratory findings
- Emphasis on transparent statistical reasoning rather than black-box performance
- Focus on demographic and admission-context predictors

### Evaluation

- Model interpretation prioritized over raw predictive accuracy
- Results assessed for clinical plausibility and consistency

---

## Limitations

- Single-center dataset limits generalizability
- Age censoring at 89 may attenuate effects among the oldest patients
- Class imbalance in cardiac arrest outcomes

---

## Repository Structure

```text
Predicting-In-Hospital-Cardiac-Arrest-in-Sepsis-Patients/
│
├── 01_data_cleaning.ipynb     # Data cleaning and cohort construction
├── data_clean_cohort.csv     # Cleaned cohort dataset exported from 01_data_cleaning
├── ADMISSIONS.csv            # Raw MIMIC-III admissions table
├── ICUSTAYS.csv              # Raw MIMIC-III ICU stays table
├── TRANSFERS.csv             # Raw MIMIC-III transfers table
├── README.md                 # Project documentation
