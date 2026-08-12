# Hiring Needs Analysis

A workforce planning and people analytics project that identifies trainer recruitment priorities by combining workforce vulnerability, operational activity, commercial demand, and estimated capacity coverage.

> **Project status:** This project is still in progress. The analytical pipeline and current decision-support outputs have been implemented, but the final interpretation of the results, an executive summary, and more detailed Markdown documentation within the notebooks are still under development.

## Overview

This project addresses one central decision:

> **Which course-location combinations should be prioritised for trainer recruitment, and how many additional trainers may be required?**

The analysis transforms workforce, training activity, lead, and sales data into two decision-support outputs:

- a ranked assessment of hiring priority for every course-location combination;
- an estimate of the minimum and recommended trainer capacity required to cover operational demand.

The intention is not to automate recruitment decisions. Instead, the project provides an interpretable framework that helps Operations, Commercial, and Recruitment teams decide where proactive sourcing, internal availability checks, or workforce reinforcement may be necessary.

## Business context

The organisation represented in this project is a professional training provider operating through multiple training centres and offering courses across several professional areas and delivery formats.

Its training workforce is composed mainly of **freelance trainers who collaborate on a service basis rather than through permanent employment contracts**. This model gives the organisation flexibility, but it also creates an important planning constraint: being registered in the trainer pool does not guarantee that a professional will be available for a particular course, date, timetable, or location.

As the organisation expands its course portfolio, geographical coverage, and digital training formats, it must be able to respond to demand without compromising the continuity of training activities. Historically, trainer recruitment could become reactive: a new enrolment or an upcoming training action would reveal that no suitable trainer was available, creating an urgent need to source and assess candidates.

This situation creates several organisational risks:

- delayed or interrupted training activities;
- excessive dependence on one or a small number of trainers;
- scheduling conflicts caused by simultaneous training actions;
- loss of commercial opportunities when demand cannot be covered;
- repeated urgent recruitment processes with limited time for sourcing and assessment;
- inefficient allocation of recruitment effort across courses and locations.

The organisation therefore required a more structured and proactive way to:

- map existing trainer coverage;
- identify vulnerable courses and locations before a shortage occurs;
- connect workforce capacity with operational and commercial demand;
- direct recruitment resources towards the most relevant priorities;
- estimate how much additional trainer capacity may be required.

## Project objectives

The main objective is to support the transition from **reactive recruitment** to **proactive, data-informed workforce planning**.

The project was developed to:

1. consolidate and validate data from different organisational areas;
2. characterise the current trainer workforce by course and location;
3. identify workforce scarcity, concentration, and shared-capacity risks;
4. measure operational pressure from training volume, recurrence, regularity, growth, and simultaneity;
5. assess commercial pressure using leads, sales, conversion, regularity, and growth;
6. combine the analytical dimensions into an interpretable hiring-priority framework;
7. estimate minimum and recommended trainer requirements for each course-location combination.

## Project status and development roadmap

The project currently contains a complete analytical workflow from data preparation to hiring prioritisation and trainer-capacity estimation. However, the repository should still be considered a **work in progress**, because the technical outputs have not yet been fully translated into a final managerial interpretation.

### Implemented

- preparation, cleaning, validation, and integration of the fictitious datasets;
- workforce, training activity, and commercial analyses;
- dimension-level scoring models;
- integration of the three dimensions into a hiring-priority assessment;
- simulation of minimum and recommended trainer-capacity requirements;
- export of intermediate scores and final decision-support datasets.

### Still in progress

- a final cross-dimensional interpretation of the results;
- an executive summary that translates the main findings into clear organisational recommendations;
- a more detailed narrative inside each notebook using Markdown sections;
- clearer explanations of the analytical decisions, assumptions, validations, transitions, and conclusions at each stage;
- a final review of the project documentation and presentation for portfolio use.

The planned executive summary will focus on the most relevant hiring priorities, the main factors driving those priorities, estimated trainer gaps, operational risks, and recommended actions for Recruitment, Operations, Commercial, and Pedagogical Coordination teams.

## Data disclaimer

> **All data in this repository are entirely fictitious and were created exclusively for analytical, educational, and portfolio purposes.**

The repository does not contain real trainers, candidates, customers, employees, commercial records, or confidential information from any organisation. Centre names are generic, and the datasets were designed to reproduce realistic workforce-planning challenges without identifying any real entity or individual.

## Analytical scope

After data preparation, the analytical universe contains:

- **24 active courses**;
- **5 training centres**;
- **120 course-location combinations**;
- **183 active trainers** in the prepared workforce dataset;
- training activity covering **2018-2026**;
- weekly lead and sales records covering **2023-2026**.

Each course-location combination is analysed independently so that the same course can receive a different priority depending on local trainer coverage and demand.

## Analytical framework

The project evaluates hiring needs through three complementary dimensions.

| Dimension | Main question | Main indicators | Weight in the hiring pressure score |
|---|---|---|---:|
| Workforce | How vulnerable is the current trainer pool? | Trainer count, relative scarcity, multi-course trainers, mobile trainers | 40% |
| Training actions | How much operational pressure does the combination generate? | Volume, growth, recurrence, regularity, concurrent actions, simultaneous action days | 40% |
| Commercial | How strongly does market demand indicate future pressure? | Leads, sales, conversion, commercial regularity, growth | 20% |

### 1. Workforce vulnerability

The workforce analysis evaluates whether trainer coverage is sufficiently diversified and locally available.

The workforce score combines:

- **Relative scarcity - 60%:** how limited the number of trainers is relative to other course-location combinations;
- **Course sharing - 20%:** the proportion of trainers who are also assigned to other courses;
- **Location sharing - 20%:** the proportion of trainers who are also available across other centres.

A higher score indicates a more vulnerable workforce structure. For example, a combination may have several trainers but still be exposed if most of them are shared with many other courses or locations.

### 2. Training activity pressure

The training actions analysis measures operational demand using both the last 12 months and the longer historical period.

The score includes:

- **Volume - 25%:** average number of actions and training hours;
- **Growth - 15%:** recent and historical changes in activity;
- **Recurrence - 15%:** how frequently new actions occur;
- **Regularity - 20%:** how consistently the course remains active over time;
- **Simultaneity - 25%:** peak concurrent actions and the proportion of days with overlapping activity.

Recent activity receives **60%** of the score and historical activity receives **40%**, preserving long-term context while giving greater relevance to current operational conditions.

### 3. Commercial pressure

Commercial analysis captures whether market interest and effective enrolments are likely to increase the need for trainer capacity.

The score includes:

- **Volume - 35%:** leads and sales generated;
- **Conversion - 25%:** the relationship between commercial interest and effective sales;
- **Regularity - 25%:** the proportion of weeks with leads and sales;
- **Growth - 15%:** recent and historical changes in commercial activity.

The recent period corresponds to the latest **13 completed weeks**. Recent and historical results are combined using weights of **60%** and **40%**, respectively.

## Hiring priority model

The final priority assessment combines two complementary perspectives.

### Weighted hiring pressure

The first score combines the three analytical dimensions:

```text
Hiring pressure = 40% Workforce + 40% Training actions + 20% Commercial
```

It also identifies the dimension that contributes most strongly to the result, making it possible to distinguish between priorities driven by workforce scarcity, operational pressure, or commercial demand.

### Cross-dimensional pressure

A second score examines demand relative to the available trainer pool. It combines:

- training hours per trainer - **30%**;
- concurrent actions per trainer - **25%**;
- weekly sales per trainer - **15%**;
- sustained demand pressure - **15%**;
- shared trainer capacity pressure - **15%**.

This perspective is useful because separate dimension scores may hide interactions. A course can appear manageable when workforce, operations, and commercial performance are examined separately, while still presenting substantial pressure when demand is divided by the trainers who can realistically cover it.

### Final priority

The final `priority_score` is the average of:

- the weighted hiring pressure score;
- the cross-dimensional hiring score.

Each combination is then classified into one of four levels:

- `Low`;
- `Lower-middle`;
- `Upper-middle`;
- `High`.

The final output also includes rankings, main pressure drivers, agreement between the two models, and an overall priority assessment.

## Trainer capacity requirements

The final notebook translates analytical priority into an estimated number of trainers.

The capacity model:

1. reconstructs every active day of each training action;
2. counts simultaneous actions for each course and location;
3. identifies trainers eligible to cover each combination;
4. accounts for trainers whose capacity is shared across simultaneous demands;
5. estimates the daily capacity gap;
6. simulates the addition of trainers;
7. selects the smallest number required to achieve defined coverage targets.

The capacity analysis separates demand into three mutually exclusive periods:

- **Historical:** activity before the most recent 12-month window;
- **Recent:** activity within the last 12 months up to the analysis date;
- **Future:** planned activity after the analysis date.

Recent and historical coverage are combined using weights of **60%** and **40%**, producing the observed weighted coverage rate. Future coverage is evaluated separately.

The final planning coverage rate is the lower of:

- the observed weighted coverage rate;
- the future coverage rate.

Two scenarios are produced:

- **Minimum requirement:** the smallest number of additional trainers required to reach at least **90% planning coverage**;
- **Recommended requirement:** the smallest number of additional trainers required to reach at least **99% planning coverage**.

This approach ensures that the recommendation is sufficient for both observed demand patterns and known future training activity.

These figures should be interpreted as planning estimates rather than guaranteed staffing requirements. Actual recruitment decisions must still consider trainer availability, timetables, delivery modality, technical certifications, course-specific requirements, compensation, and managerial judgement.

## Repository structure

```text
Hiring-Needs-Analysis/
├── data/
│   ├── raw/                         # Original fictitious Excel datasets
│   ├── processed/                   # Cleaned and transformed CSV datasets
│   ├── scores/                      # Dimension-level scored features
│   └── outputs/                     # Final decision-support datasets
├── notebooks/
│   ├── 01_data_preparation.ipynb
│   ├── 02_workforce_analysis.ipynb
│   ├── 03_actions_analysis.ipynb
│   ├── 04_commercial_analysis.ipynb
│   ├── 05_priority_analysis.ipynb
│   └── 06_trainer_capacity_requirements.ipynb
├── .gitignore
├── .python-version
├── pyproject.toml
├── uv.lock
└── README.md
```

## Notebook workflow

The notebooks should be executed in numerical order. Their technical structure is already defined, but the explanatory narrative is still being expanded. Each notebook is expected to include Markdown sections that clarify:

- the business question addressed in that stage;
- the input datasets and relevant variables;
- the cleaning, validation, feature-engineering, and scoring decisions;
- the rationale behind the selected metrics, weights, and thresholds;
- the interpretation of intermediate results and visualisations;
- how the notebook contributes to the next stage of the analysis.

This documentation is intended to make the workflow understandable not only as code, but also as a coherent analytical story connecting the organisational problem to the final recommendations.

| Notebook | Purpose |
|---|---|
| [`01_data_preparation.ipynb`](notebooks/01_data_preparation.ipynb) | Imports, cleans, validates, reshapes, and exports the processed datasets. |
| [`02_workforce_analysis.ipynb`](notebooks/02_workforce_analysis.ipynb) | Profiles trainer coverage and creates the workforce vulnerability score. |
| [`03_actions_analysis.ipynb`](notebooks/03_actions_analysis.ipynb) | Analyses training activity and creates the operational pressure score. |
| [`04_commercial_analysis.ipynb`](notebooks/04_commercial_analysis.ipynb) | Analyses leads, sales, conversion, regularity, and commercial growth. |
| [`05_priority_analysis.ipynb`](notebooks/05_priority_analysis.ipynb) | Integrates all dimensions and produces the final priority assessment. |
| [`06_trainer_capacity_requirements.ipynb`](notebooks/06_trainer_capacity_requirements.ipynb) | Estimates minimum and recommended trainer capacity requirements. |

## Main outputs

The current outputs contain the scored indicators and capacity estimates produced by the analytical pipeline. They will later be complemented by a concise executive summary with the principal findings, risks, priorities, and recommended organisational actions.

### `data/outputs/priority.csv`

The main prioritisation dataset. It contains one row per course-location combination and includes:

- final priority score and level;
- overall priority assessment;
- weighted hiring pressure and cross-dimensional pressure;
- workforce, actions, and commercial scores;
- main pressure drivers;
- workload, concurrency, commercial coverage, sustained demand, and shared-capacity indicators;
- model agreement and ranking information.

### `data/outputs/trainer_capacity_requirements.csv`

The capacity-planning dataset. It includes:

- current trainer count;
- minimum and recommended additional trainers;
- minimum and recommended total trainer capacity;
- current, minimum, and recommended coverage rates;
- recent and historical coverage;
- active-day and peak-demand indicators;
- the corresponding hiring priority assessment.

### `data/scores/`

Intermediate scored datasets are retained separately for transparency:

- `workforce_scored_features.csv`;
- `actions_scored_features.csv`;
- `commercial_scored_features.csv`.

## Technologies

- Python 3.13
- pandas
- matplotlib
- openpyxl
- JupyterLab
- uv

## Running the project

Clone the repository:

```bash
git clone https://github.com/nathansperinde/Hiring-Needs-Analysis.git
cd Hiring-Needs-Analysis
```

Install the project and development dependencies:

```bash
uv sync --all-groups
```

The notebooks use paths relative to the `notebooks/` directory. Start JupyterLab from that directory:

```bash
cd notebooks
uv run --project .. jupyter lab
```

Then execute the notebooks from `01` to `06`.

## Interpretation and limitations

This project is a decision-support system, not a prescriptive hiring model. The current datasets and scores should be treated as analytical outputs awaiting a final integrated interpretation rather than as the completed conclusion of the project.

Important limitations include:

- a trainer registered for a course or location may not be available when contacted;
- commercial interest does not necessarily become a scheduled training action;
- score weights reflect explicit analytical assumptions and can be adjusted for different organisational strategies;
- percentile-based scores express relative pressure within this dataset rather than universal thresholds;
- capacity simulations simplify real scheduling constraints and do not replace timetable-level workforce planning;
- all results are based on fictitious data and should not be interpreted as evidence about a real organisation.

The most appropriate use of the outputs is to guide further validation with operational managers, commercial teams, and recruitment professionals.

## Future development

### Additional recruitment and trainer data

A future version of the project would benefit from integrating the workforce and demand analyses with recruitment-process data. Relevant information could include:

- the training actions actually delivered by each trainer, rather than only the courses and locations for which the trainer is registered;
- the number of trainers contacted before one professional accepts a training assignment;
- trainer responses, refusals, non-responses, and stated availability;
- time required to fill each trainer need;
- recruitment source, screening stage, interview outcome, and final selection decision;
- reasons why a trainer need was not filled or required urgent sourcing;
- the relationship between candidate-pool size, contact effort, and successful coverage;
- historical changes in trainer availability by course, location, modality, timetable, and period.

These data would make it possible to distinguish nominal workforce coverage from effective workforce availability. They could also support recruitment-efficiency indicators such as contact-to-acceptance rate, time-to-fill, sourcing-channel effectiveness, and the expected number of contacts required to secure one trainer for a specific course-location combination.

### Automation and operational deployment

A longer-term objective is to automate the complete analytical process. This could be developed as a Python application connected to a SQL database, replacing the current notebook-based workflow with a reproducible and regularly updated data pipeline.

The automated solution could:

- ingest and validate workforce, training activity, commercial, and recruitment data;
- store historical and current records in a structured SQL database;
- execute feature engineering and score calculations automatically;
- update hiring priorities and trainer-capacity estimates on a scheduled basis;
- preserve calculation history and audit changes in scores over time;
- generate alerts when a course-location combination reaches a defined risk level;
- expose results through an API or internal analytical service;
- feed an interactive dashboard for managers and operational teams;
- support filters, drill-down analyses, trend monitoring, and scenario simulations.

The dashboard could present priority tiers, score drivers, current trainer coverage, estimated capacity gaps, commercial and operational trends, recruitment funnel indicators, and the evolution of risk over time.

### Further analytical extensions

Other potential developments include:

- probabilistic modelling of freelance trainer availability;
- seasonal demand forecasting;
- sensitivity analysis for score weights and coverage targets;
- timetable-level optimisation;
- scenario analysis for changes in demand or trainer availability;
- validation of model recommendations against actual recruitment and training outcomes.

## Author

Developed by [Nathan Sperinde](https://github.com/nathansperinde).
