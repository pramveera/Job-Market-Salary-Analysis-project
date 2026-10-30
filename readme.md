# Job Market & Salary Analysis

**Analyzing job market trends, salary patterns, experience levels, and in-demand technical skills using LinkedIn job postings.**

## Project Overview

This project analyzes LinkedIn job postings from 2023–2024 to understand hiring trends, salary distributions, job requirements, and technical skills demanded by employers.

The project uses Python, Pandas, NumPy, Matplotlib, Seaborn, and SQL-related data analysis concepts to transform raw job-posting data into meaningful insights.

The findings can help students and job seekers understand the skills employers request and make more informed career-development decisions.

## Objectives

- Analyze job postings by title, location, work type, and experience level.
- Investigate salary distributions across different job roles and experience levels.
- Identify salary outliers and potential salary-data quality issues.
- Identify in-demand technical skills for Data Scientist, Data Analyst, and Machine Learning Engineer roles.
- Explore relationships between job requirements, experience, and compensation.
- Develop a reproducible data-cleaning and analysis workflow.

## Dataset

**Source:** Kaggle — LinkedIn Job Postings (2023–2024)

The original `postings.csv` dataset contains approximately **123,849 job postings and 31 columns**.

Important fields include:

| Column | Description |
|---|---|
| `job_id` | Unique job-posting identifier |
| `company_name` | Company associated with the posting |
| `title` | Job title |
| `description` | Job description |
| `location` | Job location |
| `formatted_work_type` | Employment type, such as full-time or part-time |
| `formatted_experience_level` | Required experience level |
| `min_salary` | Minimum listed salary |
| `max_salary` | Maximum listed salary |
| `pay_period` | Salary period, such as hourly or yearly |
| `currency` | Salary currency |
| `normalized_salary` | Salary standardized in the source dataset |

The dataset also contains related files, including company information, job-skill mappings, and skill definitions.

*Note: The dataset contains missing salary and other optional information. Results are based on the available records and the filters used in each analysis.*

## Tools and Technologies

- **Python** — Data analysis and processing
- **Pandas and NumPy** — Data cleaning, transformation, and aggregation
- **Matplotlib and Seaborn** — Data visualization
- **Jupyter Notebook** — Exploratory analysis and documentation
- **SQL** — Relational data analysis concepts
- **Git and GitHub** — Version control and project sharing

## Project Structure

```text
Job Market & Salary Analysis project/
│
├── data/
│   ├── raw/
│   │   └── postings.csv
│   └── processed/
│       └── cleaned_job_postings.csv
│
├── notebooks/
│   ├── 01_data_inspection.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_exploratory_data_analysis.ipynb
│   └── 04_skill_demand_analysis.ipynb
│
├── reports/
│
├── README.md
└── requirements.txt
```

*The structure above represents the intended organization. Update filenames if your actual project differs.*

## Analysis Workflow

### 1. Data Inspection

- Loaded and examined the original dataset.
- Reviewed dataset dimensions, column names, and data types.
- Investigated missing values and duplicate job identifiers.

### 2. Data Cleaning

- Standardized text columns by trimming whitespace.
- Converted empty strings into missing values.
- Checked duplicate job IDs and salary-range consistency.
- Investigated missing salary information without deleting postings solely because optional fields were missing.
- Converted geographic and company identifiers to string data types.
- Added a salary-quality review flag for suspicious hourly salary-normalization patterns.
- Saved the processed dataset as `cleaned_job_postings.csv`.

**Cleaning result:** 123,849 rows and 32 columns, with no duplicate job IDs or remaining empty strings in the checked text columns.

### 3. Exploratory Data Analysis

Explored job-market characteristics, including:

- Most frequent job titles.
- Job postings by experience level.
- Geographic distribution of opportunities.
- Employment and work-type patterns.
- Salary availability and salary distributions.

### 4. Salary Analysis

- Compared salary distributions across experience levels.
- Investigated salary ranges and high-value observations.
- Examined salary differences across job titles.
- Investigated suspicious normalization patterns and assessed the effect of extreme values on summary statistics.

Salary comparisons require consistent pay periods, currencies, and units. Salary outliers are investigated rather than automatically treated as errors.

### 5. Skill-Demand Analysis

Focused on Data Scientist, Data Analyst, and Machine Learning Engineer postings.

A keyword-based approach was used to identify mentions of technical skills in job descriptions, including:

- Python and SQL
- Machine Learning and Deep Learning
- Statistics and Data Analysis
- Excel, Tableau, and Power BI
- AWS and Azure
- PyTorch and TensorFlow
- Spark, Docker, and NLP

The analysis compares skill mentions across the selected roles to identify potentially useful learning priorities.

**Important limitation:** Skill counts represent keyword mentions in the selected postings, not a complete census of all job-market requirements. Keyword extraction may miss synonyms or context and may count a skill even when it is not a strict requirement.

## Key Findings

- The dataset contains **123,849 job postings**.
- Mid-Senior was the largest experience-level group in the analyzed dataset.
- Salary information was available for approximately **36,073 postings**.
- Python and SQL were among the most frequently detected technical skills in the selected data-related job postings.
- Salary records showed potential inconsistencies between hourly labels, raw salary values, and normalized salaries.
- Missing values are common and need to be considered when interpreting each analysis.

These findings are descriptive and depend on the dataset, filters, and extraction methods used.

## How to Run the Project

### 1. Clone the repository

```bash
git clone <your-github-repository-url>
cd "Job Market & Salary Analysis project"
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

Activate it on Windows:

```bash
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Add the dataset

Download the dataset from Kaggle and place the required raw files in the `data/raw/` directory.

### 5. Run the notebooks

Open Jupyter Notebook or VS Code and run the notebooks in sequence, starting with data inspection and cleaning.

If you already have the processed dataset, you can use it for subsequent analysis notebooks.

## Limitations

- The dataset represents the collected LinkedIn postings, not every job available in the labor market.
- Salary information is missing for many postings.
- Salary values may use different currencies, pay periods, or units.
- Some unusually large salary values require further investigation.
- Skill extraction uses keywords and may not capture every skill or its context.
- Results should be interpreted as exploratory findings rather than definitive labor-market estimates.

## Future Improvements

- Build interactive dashboards with Streamlit or Power BI.
- Improve skill extraction using NLP techniques.
- Compare skills and compensation across job roles and experience levels.
- Analyze changes in skill demand over time where timestamps support reliable comparisons.
- Add a salary-quality validation pipeline.
- Integrate job-market insights into an AI-powered career guidance platform.

## Author

**Pramveer Kumar**

B.Tech — Computer Science and Engineering (Artificial Intelligence)

---

*This project is developed for data-analysis practice, portfolio development, and understanding job-market requirements.*
