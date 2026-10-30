# Job Market & Salary Analysis — Project Report

## 1. Executive Summary

This project analyzes LinkedIn job postings from 2023–2024 to explore job-market patterns, salary information, experience levels, and technical skills mentioned in selected data-related job descriptions.

The original postings dataset contains 123,849 records and 31 columns. A cleaned version was produced with 123,849 records and 32 columns, including a salary-quality review flag. The analysis includes job-market exploration, salary analysis, and keyword-based skill-demand analysis for Data Scientist, Data Analyst, and Machine Learning Engineer roles.

## 2. Project Objectives

- Understand the distribution of job postings by title, location, work type, and experience level.
- Explore salary distributions and differences across experience levels and job titles.
- Investigate unusual salary values and potential data-quality issues.
- Identify commonly mentioned technical skills in selected data-related job postings.
- Build a reproducible Python data-cleaning and analysis workflow.

## 3. Dataset

**Source:** Kaggle — LinkedIn Job Postings (2023–2024).

The `postings.csv` file used in this project contains 123,849 job postings and 31 columns. Important fields include:

- `job_id`: job-posting identifier
- `company_name`: company name
- `title`: job title
- `description`: job description
- `location`: job location
- `formatted_work_type`: work arrangement/employment type
- `formatted_experience_level`: experience level
- `min_salary`, `max_salary`, `med_salary`: salary fields
- `pay_period`: salary period
- `currency`: salary currency
- `normalized_salary`: source-provided normalized salary

Related dataset files, including job-skill mappings and skill definitions, were also explored for skill analysis.

## 4. Tools and Libraries

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

The exact installed package versions can be recorded with `pip freeze` when the project environment is finalized.

## 5. Methodology

### 5.1 Data inspection

The raw postings file was loaded and inspected for its dimensions, columns, data types, missing values, and duplicate job identifiers.

### 5.2 Data cleaning

A working copy (`clean_df`) was created so that the original raw DataFrame remained unchanged.

Cleaning and validation steps included:

- Trimming whitespace from text columns.
- Replacing empty strings with missing values.
- Checking duplicate job IDs.
- Checking for negative salary values.
- Checking whether minimum salary exceeded maximum salary.
- Reviewing missing salary information by pay period and currency.
- Converting `company_id`, `zip_code`, and `fips` to string identifiers.
- Adding a salary-quality review flag for a systematic hourly normalization pattern.
- Saving and reloading the processed CSV to verify the output.

**Cleaning validation results:**

| Check | Result |
|---|---:|
| Rows in cleaned dataset | 123,849 |
| Columns in cleaned dataset | 32 |
| Duplicate job IDs | 0 |
| Empty strings remaining in checked text columns | 0 |
| Rows deleted during cleaning | 0 |
| Records flagged for salary review | 10,212 |

Missing values were retained where the information was not supplied. Missing salary values were not replaced with zero or imputed.

### 5.3 Salary-quality investigation

The dataset contained 10,212 hourly postings with non-missing minimum salary, maximum salary, and normalized salary values. For all 10,212 records, the ratio of normalized salary to the raw salary midpoint was exactly 2,080.

The factor 2,080 corresponds to 40 working hours per week multiplied by 52 weeks. This indicates a systematic unit or normalization inconsistency in these records. The project flags these rows for review rather than assuming which source field is incorrect or changing the original values.

The flag is a review indicator, not proof that every flagged raw salary is invalid.

### 5.4 Exploratory data analysis

Previously completed EDA explored job titles, locations, experience levels, work types, salary availability, salary distributions, and salary patterns across experience levels.

Reported observations include:

- Sales Manager was the most frequent job title in the analysis, with 673 postings.
- Mid-Senior was the largest experience-level category, with 41,489 postings.
- 36,073 postings had at least one salary field populated.

### 5.5 Salary analysis

A comparable annual salary subset was created using these conditions:

- `pay_period` was `YEARLY`.
- `currency` was `USD`.
- Minimum and maximum salaries were available.
- Salary values were non-negative.
- Maximum salary did not exceed $1,000,000.

This subset contained 19,084 postings. Salary midpoint was calculated as:

`(min_salary + max_salary) / 2`

Summary statistics for the subset:

| Metric | Value |
|---|---:|
| Number of postings | 19,084 |
| Mean salary midpoint | $116,350.46 |
| Median salary midpoint | $105,000 |
| IQR outliers identified | 622 |
| IQR outlier share | 3.26% |

In a sensitivity check excluding the 622 IQR outliers, the mean salary midpoint was approximately $109,338.41 and the median was $102,500. The outliers were investigated rather than automatically deleted from the source dataset.

Median salary midpoint by experience level in the filtered annual USD subset:

| Experience level | Median salary midpoint |
|---|---:|
| Executive | $200,000 |
| Director | $169,500 |
| Mid-Senior | $115,000 |
| Associate | $82,500 |
| Entry | $77,500 |
| Internship | $65,000 |

These statistics describe only the filtered subset and should not be interpreted as universal salary benchmarks.

### 5.6 Skill-demand analysis

Skill analysis focused on 742 postings whose titles matched Data Scientist, Data Analyst, or Machine Learning Engineer.

A keyword-based approach was used to identify skill mentions in job descriptions. Top mentions included:

| Skill | Postings mentioning skill | Share of 742 |
|---|---:|---:|
| Python | 425 | 57.28% |
| SQL | 410 | 55.26% |
| Machine Learning | 312 | 42.05% |
| Statistics | 257 | 34.64% |
| Data Analysis | 254 | 34.23% |
| Excel | 167 | 22.51% |
| Tableau | 130 | 17.52% |
| Data Visualization | 125 | 16.85% |
| AWS | 114 | 15.36% |
| PyTorch | 82 | 11.05% |

These are keyword mentions in the selected postings, not a complete census of all employer requirements. Keyword matching can miss synonyms, context, and skills expressed in different ways.

## 6. Key Findings

1. The dataset provides a substantial sample of job postings for descriptive job-market analysis.
2. Experience-level and job-title distributions are uneven; Mid-Senior postings form the largest experience group in the reported analysis.
3. Salary information is available for only a subset of postings, so salary comparisons require explicit filtering.
4. Salary fields contain a systematic hourly normalization pattern affecting 10,212 comparable records.
5. Python and SQL are the most frequently detected skills in the selected data-related postings.
6. Skill-demand findings depend on the selected job titles and keyword dictionary.

## 7. Limitations

- The dataset represents the collected LinkedIn postings, not the entire labor market.
- Many postings have missing salary information.
- Currency, pay period, and salary-unit inconsistencies can affect comparisons.
- The 2,080 normalization pattern is strong evidence of a systematic inconsistency, but does not by itself establish which source field is incorrect.
- Keyword-based skill extraction may miss synonyms and contextual meaning, and may count incidental mentions.
- Findings are descriptive and should not be treated as causal conclusions or guaranteed salary benchmarks.

## 8. Conclusion

The project demonstrates a practical data-science workflow: data inspection, cleaning, validation, exploratory analysis, salary analysis, feature creation, anomaly investigation, and text-based skill extraction.

The results can provide a foundation for a future career-intelligence application such as CareerPilot AI. For example, skill-demand findings could inform job-role exploration and learning-roadmap recommendations. Such integration would require additional validation and potentially richer job and skills data.

## 9. Reproducibility and Project Files

The processed dataset is saved as:

`data/processed/cleaned_job_postings.csv`

The original raw dataset should remain in:

`data/raw/`

Recommended notebook sequence:

1. `01_data_inspection.ipynb`
2. `02_data_cleaning.ipynb`
3. `03_exploratory_data_analysis.ipynb`
4. `04_skill_demand_analysis.ipynb`

Run the notebooks from the project environment and ensure the dataset paths match the actual folder structure.
