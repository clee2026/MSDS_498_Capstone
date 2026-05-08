# NYC 311 Data Pipeline - Notebook Workflow

## Purpose

This project follows a structured pipeline to move from raw NYC 311 data to a model-ready dataset and final analysis outputs.

Instead of jumping directly into modeling, the process is broken into three notebooks so that:

- field selection is based on actual data behavior  
- data preparation is consistent and documented  
- modeling results are reliable and reproducible  

---

## Pipeline Overview
- Notebook 1 -> Notebook 2 -> Notebook 3
- Raw Parquet -> Data Conditioning -> Model-Ready Data -> Analysis + Modeling


---

## Notebook 1 - Data Understanding (EDA)

### Purpose

Notebook 1 answers:

> What data do we actually have, and which fields are usable?

This step avoids guessing and replaces it with measured decisions.

---

### Key Tasks

- Profile all columns using the full dataset (~20M records)
- Measure:
  - missing values
  - distributions
  - cardinality
- Identify:
  - usable fields
  - low-value or redundant fields
  - high-missingness fields

---

### Outputs

- `column_profile.csv`  
  -> summary of each column (type, unique values, etc.)

- `missingness_summary.csv`  
  -> % missing for each field

- `candidate_drop_review.csv`  
  -> recommendation: keep / drop / review

---

### Important

This step ensures:

- field selection is **data-driven**
- so not relying on the data dictionary alone
- downstream steps are justified in the report

---

## Notebook 2 - Data Conditioning (Step 2 Focus)

### Purpose

Notebook 2 answers:

> How do we transform the raw dataset into a clean, model-ready dataset?

This is the **core step for the meeting**.

---

### Meeting Objective (Step 2)

At the end of this step, should have:

- a final list of columns to **keep**
- a list of columns to **drop**
- a list of columns to **modify**
- a list of **new features** to add

This creates a consistent dataset for all modeling work.

---

### Key Tasks

#### 1. Column Selection
- Use Notebook 1 outputs to finalize:
  - keep columns
  - drop columns

#### 2. Data Cleaning
- Handle missing values:
  - categorical → `"UNKNOWN"`
  - numeric → median
- Standardize formats:
  - datetime
  - categorical values

#### 3. Feature Engineering

Create modeling features such as:

- `response_time_hours`
- `closed_same_day_flag`
- `repeat_complaint_flag`

#### 4. Sampling Strategy

- Use a **representative sample** (not all 20M rows)
- Enables modeling in standard Colab environment

---

### Outputs

- `analysis_ready_sample.parquet`  
  -> clean dataset used for modeling

- `final_field_list.csv`  
  -> final list of selected columns

- `missing_value_treatment.csv`  
  -> how missing values were handled

- `derived_features_summary.csv`  
  -> definitions of new features

---

### Important

This step ensures:

- ready to use **dataset**
- transformations are **documented and reproducible**
- modeling is based on **clean, structured data**

---

## Notebook 3 - Analysis + Modeling

### Purpose

Notebook 3 answers:

> What insights does the data provide, and what can we predict?

This is where results are generated for the report.

---

### Key Tasks

#### 1. Full Dataset Aggregation (20M records)

Run batch processing to compute:

- complaint volume
- borough distribution
- time trends

#### 2. Sample-Based Analysis

Use the prepared sample to analyze:

- response time behavior
- delay patterns

#### 3. Modeling

Build models for:

- Regression -> `response_time_hours`
- Classification -> `closed_same_day_flag`

---

### Outputs

#### Full Dataset Outputs
- `full_counts_complaint_type.csv`
- `full_counts_borough.csv`
- `full_monthly_counts.csv`

#### Sample Analysis Outputs
- `sample_response_time_summary.csv`
- `sample_response_by_complaint_type.csv`

#### Modeling Outputs
- `regression_model_metrics.csv`
- `classification_model_metrics.csv`
- feature importance plots
- confusion matrices

#### Final Summary
- `top_findings_table.csv`

## Notebook 4 - Operational Clustering + Trend Analysis

### Purpose

Notebook 4 answers:

> What operational complaint environments exist, and how do they change over time?

This step extends the supervised modeling by identifying:

- recurring complaint hotspots
- operational service segments
- geographic workload concentration
- response time trends
- seasonal and recurring complaint behavior

The goal is not simply clustering for machine learning purposes, but operational intelligence that management can use for planning and resource allocation.

---

### Key Tasks

#### 1. Geographic Clustering

Use complaint latitude and longitude to identify:

- complaint hotspots
- recurring operational regions
- geographic service concentration

#### 2. Operational Segmentation

Group complaints by operational behavior using variables such as:

- response time
- same-day closure
- complaint type
- borough
- repeat complaint behavior

Clusters are translated into operational segment labels for report readability and management interpretation.

#### 3. Repeat Complaint Proxy Analysis

Create operational indicators for recurring complaint environments using:

- complaint type
- geographic proximity
- recurring complaint patterns

#### 4. Operational Trend Analysis

Analyze trends across operational segments including:

- complaint volume trends
- response time trends
- recurring complaint behavior
- emerging hotspot growth
- seasonal workload patterns

---

### Outputs

#### Geographic Clustering Outputs
- `geo_cluster_summary_report_ready.csv`
- `geo_hotspot_top15_report_labels.png`

#### Operational Segmentation Outputs
- `operational_segment_summary_report_ready.csv`
- `operational_segment_avg_response_time_report_labels.png`
- `operational_segment_same_day_rate_report_labels.png`
- `operational_segment_complaint_type_heatmap_report_labels.png`

#### Trend Analysis Outputs
- `trend_operational_segment_monthly_volume.csv`
- `trend_operational_segment_avg_response_time.csv`
- `trend_operational_segment_monthly_volume.png`
- `trend_operational_segment_avg_response_time.png`
- `top_trending_complaint_types.csv`
- `emerging_hotspot_summary.csv`

---

### Important

This step provides:

- operational segmentation
- geographic intelligence
- recurring complaint analysis
- management-focused trend analysis
- seasonal preparedness insights
- proactive planning support

The clustering and trend analysis complements the supervised models by explaining how operational environments behave over time rather than only predicting outcomes.

---

### Important

This step provides:

- report-ready insights  
- measurable patterns in the data  
- predictive capabilities  

---

## Key Principle

Most workflows:
- load data -> explore -> guess fields -> model

This workflow:
- profile -> validate -> select -> clean -> engineer -> analyze -> model
