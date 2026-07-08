# Predicting In-Hospital Cardiac Arrest in Sepsis Patients

This project explores whether routinely collected electronic health record (EHR) data can help identify cardiac arrest risk among ICU patients with sepsis. Using selected tables from the MIMIC-III clinical database, the analysis builds a cleaned cohort, performs exploratory data analysis, and evaluates interpretable statistical models focused on age, admission context, and ICU length of stay.

The goal of this repository is not to deploy a clinical model, but to demonstrate a reproducible clinical risk prediction workflow: defining a cohort, cleaning messy healthcare data, testing preregistered hypotheses, and interpreting results with appropriate caution.

## Research Question

**Can early-available patient and admission features be used to identify cardiac arrest risk among sepsis patients?**

The project also investigates two focused questions:

- Are older patients, particularly patients over 65, associated with different odds of cardiac arrest?
- Does cardiac arrest status correspond to differences in ICU length of stay?

## Dataset

This project uses data derived from the **MIMIC-III Clinical Database v1.4**, a de-identified critical care database from Beth Israel Deaconess Medical Center.

| File | Description |
| --- | --- |
| `ADMISSIONS.csv` | Hospital admission-level information, including admission type, diagnosis text, ethnicity, and timestamps |
| `ICUSTAYS.csv` | ICU stay-level information, including ICU identifiers and length of stay |
| `TRANSFERS.csv` | Transfer-level information describing movement between hospital care units |
| `data_clean_cohort.csv` | Cleaned cohort export used for downstream analysis |

Access to the full MIMIC-III database requires completion of approved training and a data use agreement through PhysioNet.

**Important data note:** the available diagnosis fields identify patients admitted with sepsis or cardiac arrest diagnoses. They do not directly identify the exact time of an in-hospital cardiac arrest event. Because of this, the analysis should be interpreted as an exploratory association study rather than a fully validated real-time early warning system.

## Methods

### 1. Cohort Construction

The cleaning notebook combines admissions, ICU stays, and transfer records using shared patient and admission identifiers. The cohort is filtered using diagnosis text for:

- Sepsis-related admissions
- Cardiac arrest-related admissions

The notebook reports:

- **2,516** sepsis patients
- **377** cardiac arrest patients
- **2,893** combined cohort records before final downstream filtering/export

### 2. Exploratory Data Analysis

The project examines:

- ICU length-of-stay distributions
- Admission type distribution
- Mortality patterns by patient group
- Missingness patterns
- ICU care unit distribution
- Basic correlation patterns among engineered variables

### 3. Statistical Modeling

The final notebook uses interpretable statistical tests rather than black-box machine learning models:

| Question | Method | Main Result |
| --- | --- | --- |
| Is age over 65 associated with cardiac arrest? | Logistic regression with `AGE65_PLUS` | OR = 0.77, 95% CI = 0.62-0.95, p = 0.0168 |
| Is continuous age associated with cardiac arrest? | Logistic regression with `AGE_AT_ADMIT` | OR = 0.990 per year, 95% CI = 0.984-0.997, p = 0.0030 |
| Does ICU length of stay differ by arrest status? | OLS regression and Mann-Whitney U test | OLS was not significant; Mann-Whitney U p = 0.0471 |

## Key Findings

- Age was statistically associated with cardiac arrest status in both age models.
- The direction of the age association was opposite the initial hypothesis: older patients had slightly lower observed odds of cardiac arrest in this cohort.
- ICU length-of-stay distributions differed between arrest and non-arrest groups according to the Mann-Whitney U test, even though the OLS mean comparison was not statistically significant.
- Admission type was highly imbalanced, with the majority of records classified as emergency admissions, limiting the strength of admission-type comparisons.

These findings should be treated as exploratory. They suggest measurable associations in the cleaned cohort, but they do not establish clinical causality or deployment-ready predictive performance.

## Repository Structure

```text
.
├── 01_data_cleaning.ipynb          # Loads, merges, cleans, and explores the raw MIMIC-III tables
├── Clinical-Risk-Prediction.ipynb  # Final statistical analysis and interpretation
├── ADMISSIONS.csv                  # Raw admissions table subset
├── ICUSTAYS.csv                    # Raw ICU stays table subset
├── TRANSFERS.csv                   # Raw transfer table subset
├── data_clean_cohort.csv           # Cleaned cohort export
├── requirements.txt                # Python dependencies for running the notebooks
└── README.md                       # Project overview and documentation
```

## How to Run

1. Clone the repository.

   ```bash
   git clone https://github.com/lindagu1/Predicting-In-Hospital-Cardiac-Arrest-in-Sepsis-Patients.git
   cd Predicting-In-Hospital-Cardiac-Arrest-in-Sepsis-Patients
   ```

2. Install the required Python packages.

   ```bash
   pip install -r requirements.txt
   ```

3. Open the notebooks in Jupyter Notebook, JupyterLab, VS Code, or Google Colab.

4. Run the notebooks in this order:

   ```text
   01_data_cleaning.ipynb
   Clinical-Risk-Prediction.ipynb
   ```

## Limitations

- MIMIC-III is a single-center ICU dataset, so results may not generalize to other hospitals or patient populations.
- The current diagnosis-based cohort does not capture exact in-hospital cardiac arrest event timing.
- Age values above 89 are affected by MIMIC-III de-identification practices.
- Admission type is highly imbalanced, which limits comparisons between emergency, urgent, and elective admissions.
- The models use static demographic and admission-level variables rather than richer time-series vitals, labs, and treatment data.
- Statistical significance does not necessarily imply clinical significance.

## Future Work

- Incorporate time-series data from vitals and labs to better support early warning prediction.
- Define cardiac arrest timing more precisely using additional MIMIC-III tables.
- Add model validation with train/test splits or cross-validation.
- Evaluate clinically relevant metrics such as sensitivity, specificity, AUROC, and calibration.
- Compare interpretable models with machine learning approaches after improving feature availability.

## Citation

Johnson, A. E. W., Pollard, T. J., Shen, L., Lehman, L. H., Feng, M., Ghassemi, M., Moody, B., Szolovits, P., Celi, L. A., & Mark, R. G. (2016). *MIMIC-III, a freely accessible critical care database*. Scientific Data, 3, 160035. https://doi.org/10.1038/sdata.2016.35

MIMIC-III Clinical Database v1.4: https://physionet.org/content/mimiciii/1.4/
