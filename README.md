# Classify Suspected Infection in Patients

## Project Overview

This project analyzes electronic health record (EHR) data to identify patients with suspected severe infections using machine learning criteria. The goal is to develop a reliable method for flagging patients who may have sepsis, a deadly syndrome where severe infection causes organ failure.

## Problem Statement

Sepsis is challenging to recognize but early treatment significantly improves survival rates. This project uses two weeks of hospital EHR data to identify patients who had severe infections according to four specific criteria, which could help in developing predictive algorithms for sepsis detection.

## Dataset Description

The project uses three main datasets:

### 1. `all_patients.csv`
- Contains patient IDs for all patients hospitalized during the two-week period
- 892 total patients
- Primary key: `patient_id`

### 2. `antibioticDT.csv`
- Records of all antibiotic administrations over two weeks
- 6,791 records
- Columns:
  - `patient_id`: Patient identifier
  - `day_given`: Day of hospitalization when antibiotic was given
  - `antibiotic_type`: Type of antibiotic (e.g., ciprofloxacin, doxycycline, penicillin)
  - `route`: Administration route (IV, PO)

### 3. `blood_cultureDT.csv`
- Records of blood culture tests performed
- 789 records
- Columns:
  - `patient_id`: Patient identifier
  - `blood_culture_day`: Day of hospitalization when blood culture was performed

## Methodology

### Criteria for Suspected Infection

The project identifies patients with suspected severe infections using four criteria:

1. **Four-day antibiotic sequence**: Patient receives antibiotics for a sequence of four days, with gaps of one day allowed
2. **New antibiotic requirement**: Sequence must start with a "new" antibiotic (not given in the previous two days)
3. **Blood culture proximity**: Sequence must start within two days of a blood culture
4. **IV antibiotic requirement**: At least one intravenous (IV) antibiotic must be given within the ±2 day window

### Analysis Steps

1. **Identify new antibiotics**: Determine which antibiotic administrations represent "new" antibiotics based on prior administration history
2. **Merge datasets**: Combine antibiotic and blood culture data to find patients in both datasets
3. **Window analysis**: Identify antibiotic administrations within ±2 days of blood cultures
4. **IV requirement check**: Ensure at least one IV antibiotic is given in the window
5. **Sequence identification**: Find qualifying four-day antibiotic sequences starting with new antibiotics
6. **Consecutive sequence validation**: Verify sequences have no gaps greater than one day
7. **Prevalence calculation**: Determine the percentage of all patients meeting the criteria

## Results

The analysis found that **0.00%** of patients met all criteria for suspected infection during the two-week period.

## Technical Implementation

- **Language**: Python
- **Key Libraries**: pandas
- **Data Processing**: Data merging, grouping, filtering, and sequence analysis
- **Analysis Type**: Descriptive statistics and pattern recognition

## Files Structure

```
├── datasets/
│   ├── all_patients.csv          # All patient IDs
│   ├── antibioticDT.csv          # Antibiotic administration records
│   ├── blood_cultureDT.csv       # Blood culture test records
│   ├── iris.csv                  # Additional dataset (not used in main analysis)
│   └── simulate_ehr_data.R       # R script for data simulation
├── notebook.ipynb                # Main analysis notebook
└── README.md                     # Project documentation
```

## Usage

1. Ensure all datasets are in the `datasets/` folder
2. Run the Jupyter notebook `notebook.ipynb` to execute the complete analysis
3. The notebook contains step-by-step implementation of the infection classification criteria

## Future Applications

This methodology could be extended to:
- Develop real-time sepsis detection algorithms
- Create early warning systems for hospital staff
- Improve patient outcomes through faster infection identification
- Support clinical decision-making processes

## References

The criteria for suspected infection are based on research published in the National Center for Biotechnology Information (NCBI) database.