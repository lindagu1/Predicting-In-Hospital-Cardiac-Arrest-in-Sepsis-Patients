# Predicting-In-Hospital-Cardiac-Arrest-in-Sepsis-Patients
Machine learning–based risk prediction using EHR data from the MIMIC-III clinical database.

# Predicting In-Hospital Cardiac Arrest in Sepsis Patients

## Overview

This repository contains a Phase V research project that investigates the prediction of **in-hospital cardiac arrest among sepsis patients** using electronic health record (EHR) data. The project leverages the MIMIC-III clinical database to explore patient characteristics, admission context, and clinical variables associated with elevated cardiac arrest risk.

The work is framed as a clinical risk prediction study with an emphasis on transparent analysis, statistical reasoning, and reproducibility.

---

## Primary Research Question

**Can patient demographics and admission-related factors be used to predict in-hospital cardiac arrest among patients diagnosed with sepsis?**

---

## Key Findings

* **Age** is a strong predictor of in-hospital cardiac arrest among sepsis patients.
* **Emergency admissions** are associated with a higher arrest risk compared to urgent admissions.
* Admission context and patient demographics may serve as useful early indicators for risk stratification models.

These findings suggest that relatively simple features available early in a hospital stay may carry a meaningful predictive signal.

---

## Data Source

* **MIMIC-III Clinical Database**
* De-identified ICU patient data from a single tertiary-care hospital
* Age values capped at 89 years to comply with HIPAA de-identification standards

Access to MIMIC-III requires credentialing and completion of required training.

---

## Methodology

1. **Data Cleaning & Cohort Construction**

   * Filtered admissions for sepsis patients
   * Identified in-hospital cardiac arrest outcomes
   * Processed demographic and admission-related variables

2. **Exploratory Data Analysis**

   * Distributional analysis of age and admission types
   * Outcome prevalence across patient subgroups

3. **Modeling Approach**

   * Iterative model development informed by exploratory findings
   * Initial modeling followed by a project pivot after group reassessment
   * Final models focused on interpretable predictors

4. **Evaluation**

   * Model interpretation prioritized over raw predictive performance
   * Results analyzed in the context of clinical plausibility

---

## Limitations

* Single-center dataset limits generalizability
* Age censoring at 89 may attenuate effects in the oldest patients
* Admission-type distribution imbalance

---

## Repository Structure

```
├── Phase_V.ipynb        # Main analysis notebook
├── README.md           # Project overview and documentation
```

---

## Reproducibility

All analysis is contained within the Jupyter notebook. The project is designed to be:

* Fully reproducible given access to MIMIC-III
* Transparent in assumptions and modeling choices
* Suitable for academic review or instructional use
