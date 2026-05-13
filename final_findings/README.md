# NYC 311 Predictive Operations Analytics Pipeline

This repository contains a multi stage analytics and machine learning pipeline developed for large scale NYC 311 operational analysis. The workflow progresses from full dataset intake and validation through data conditioning, predictive modeling, clustering analysis, operational hotspot detection, and trend analysis.

The notebooks were designed to support operational intelligence, predictive service management, workload prioritization, staffing optimization, and long term scalability planning for high volume municipal service request environments.

The overall pipeline follows the structure below:

1. Full dataset intake and profiling
2. Representative sampling and conditioning
3. Predictive delay risk and response time modeling
4. Operational clustering, hotspot analysis, and trend analysis

---

# Notebook 1 v3

# Full Dataset Intake Profiling and Representative Sampling Check

## Overview

Notebook 1 performs the initial ingestion, validation, profiling, and exploratory assessment of the NYC 311 parquet dataset. The notebook establishes the foundational operational understanding required for downstream modeling and analytics.

The notebook validates parquet structure, profiles missingness behavior, evaluates schema consistency, generates representative operational samples, and produces baseline operational summaries used throughout the remainder of the pipeline.

This notebook functions as the primary intake and audit layer for the project.

---

## Primary Objectives

* Validate source parquet integrity
* Profile dataset structure and schema consistency
* Evaluate missingness patterns across operational fields
* Generate representative operational samples
* Produce baseline operational distributions
* Create reusable metadata manifests for downstream notebooks
* Generate operational summary outputs for reporting and visualization

---

## Core Workflow

### 1. Dataset Intake and Validation

The notebook validates the source parquet dataset before analytical processing begins.

Validation activities include:

* Source parquet existence checks
* Row group inspection
* Schema extraction
* Column inventory generation
* Basic dataset metadata validation
* Memory aware loading procedures

The notebook supports very large parquet datasets through row group aware sampling and incremental loading logic.

---

### 2. Representative Operational Sampling

A representative operational sample is generated across the full parquet dataset.

The sampling process was designed to:

* Preserve operational diversity
* Maintain borough representation
* Maintain complaint type variation
* Preserve temporal variability
* Reduce memory pressure during modeling
* Support scalable experimentation

The resulting sample becomes the analytical foundation for downstream conditioning and modeling notebooks.

---

### 3. Missingness Profiling

The notebook profiles null distributions and missing operational fields.

This process helps identify:

* High risk fields
* Sparse operational attributes
* Potential modeling exclusions
* Data quality concerns
* Candidate transformation fields

Missingness summaries are exported for reporting and downstream feature engineering decisions.

---

### 4. Operational Distribution Analysis

The notebook generates operational distribution summaries including:

* Complaint type frequency
* Borough distributions
* Date coverage analysis
* Top categorical value distributions
* Basic workload concentration analysis

These summaries establish the initial operational context used later in hotspot analysis and predictive modeling.

---

## Key Outputs

### Data Outputs

| Output File                             | Description                                                       |
| --------------------------------------- | ----------------------------------------------------------------- |
| `profile_sample_representative.parquet` | Representative operational sample generated from the full dataset |
| `schema_columns.csv`                    | Extracted parquet schema and column inventory                     |
| `parquet_inventory.csv`                 | Dataset structure and parquet inventory summary                   |
| `full_dataset_missingness_profile.csv`  | Missingness summary across operational fields                     |
| `top_values_{c}.csv`                    | Top categorical value summaries for selected columns              |
| `date_coverage_{c}.csv`                 | Temporal coverage summaries                                       |
| `run_manifest.json`                     | Shared metadata manifest used by downstream notebooks             |

---

### Visualization Outputs

| Visualization                            | Purpose                               |
| ---------------------------------------- | ------------------------------------- |
| `missingness_top25.png`                  | Top missing operational fields        |
| `top_complaint_types_profile_sample.png` | Complaint type concentration analysis |

---

## Operational Value

This notebook establishes the operational baseline required for the remainder of the analytics pipeline.

Key management insights generated during intake profiling include:

* Identification of dominant operational workload categories
* Detection of high volume complaint environments
* Identification of sparse operational fields unsuitable for modeling
* Establishment of representative analytical sampling procedures
* Early identification of operational concentration patterns

The profiling process also reduces downstream modeling instability by identifying problematic operational attributes before feature engineering begins.

---

## Technical Highlights

* Row group aware parquet processing
* Memory efficient large scale dataset handling
* Incremental sampling architecture
* Automated schema extraction
* Automated operational profiling
* Manifest driven pipeline coordination
* Export oriented workflow for reproducibility

---

## Downstream Dependencies

Notebook 1 produces the shared `run_manifest.json` file required by Notebook 2.

The outputs generated here provide:

* Source dataset references
* Schema metadata
* Representative operational samples
* Initial profiling statistics

---

## Recommended Use Cases

* Large scale operational data auditing
* Municipal service request profiling
* Exploratory operational intelligence
* Baseline workload assessment
* Initial feature selection planning
* Dataset readiness validation for machine learning

---

# Notebook 2 v3

# Data Conditioning, Full Dataset Aware Sampling, and Corrected Repeat Proxy

## Overview

Notebook 2 transforms the raw operational dataset into analysis ready and modeling ready datasets through structured conditioning, operational filtering, feature engineering, and repeat complaint proxy generation.

This notebook functions as the primary feature engineering and analytical conditioning layer within the pipeline.

The notebook performs scalable operational transformations designed specifically for large scale municipal service request environments.

---

## Primary Objectives

* Normalize operational fields
* Condition high variance operational attributes
* Create repeat complaint proxy features
* Generate model ready datasets
* Apply operational filtering logic
* Create engineered response time metrics
* Produce reusable analysis ready outputs
* Support predictive modeling and clustering workflows

---

## Core Workflow

### 1. Manifest Driven Dataset Loading

The notebook loads the shared metadata manifest produced by Notebook 1.

This ensures:

* Consistent source dataset references
* Reproducible processing
* Coordinated multi notebook execution
* Stable dataset lineage

---

### 2. Column Normalization and Cleaning

Operational fields are standardized and normalized to improve downstream analytical consistency.

Normalization tasks include:

* Column naming cleanup
* Datetime conversion
* String normalization
* Null handling
* Categorical standardization
* Filtering invalid operational records

---

### 3. Repeat Complaint Proxy Engineering

A corrected repeat complaint proxy workflow is implemented using full dataset aware aggregation logic.

The repeat proxy process identifies operational environments associated with recurring complaint behavior.

This process helps identify:

* Chronic operational environments
* Repeat workload concentration
* Potential service inefficiencies
* High recurrence complaint patterns

Repeat complaint proxy features later become important drivers in operational hotspot analysis and predictive modeling.

---

### 4. Response Time Engineering

Operational response time metrics are engineered from service request lifecycle timestamps.

The notebook calculates:

* Response duration
* Delay indicators
* Percentile based delay thresholds
* Operational timing distributions

Percentile based conditioning is applied to stabilize long tailed operational behavior.

---

### 5. Modeling Dataset Preparation

The notebook generates two major datasets:

| Dataset                            | Purpose                               |
| ---------------------------------- | ------------------------------------- |
| `analysis_ready_sample_v3.parquet` | Clustering and operational analysis   |
| `model_ready_sample_v3.parquet`    | Predictive machine learning workflows |

Additional operational filtering logic ensures:

* Stable target distributions
* Reduced invalid operational records
* Consistent feature availability
* Improved downstream model stability

---

## Key Outputs

### Data Outputs

\* Not stored in the repository due to size limit
| Output File                            | Description                                      |
| -------------------------------------- | ------------------------------------------------ |
| `*analysis_ready_sample_v3.parquet`    | Conditioned dataset for operational analytics    |
| `*model_ready_sample_v3.parquet`       | Modeling optimized dataset                       |
| `*full_dataset_repeat_proxy_counts.csv`| Full dataset repeat complaint proxy summary      |
| `repeat_proxy_sample_summary.csv`      | Repeat complaint sample analysis                 |
| `final_model_field_list_v3.csv`        | Final selected modeling fields                   |
| `transformation_rules_v3.csv`          | Documented transformation and conditioning rules |
| `notebook2_v3_manifest.json`           | Notebook level execution metadata                |

---

## Operational Value

Notebook 2 converts raw municipal operational records into decision ready analytical datasets.

Major operational benefits include:

* Stabilized operational timing behavior
* Improved modeling reliability
* Identification of recurring complaint environments
* Operational feature standardization
* Reduction of analytical noise
* Creation of predictive operational indicators

The repeat complaint proxy logic is particularly important because it captures operational persistence behavior often associated with backlog formation, chronic infrastructure issues, and repeated citizen dissatisfaction.

---

## Technical Highlights

* Full dataset aware aggregation logic
* Memory efficient transformation pipeline
* Percentile based outlier stabilization
* Large scale repeat proxy engineering
* Structured feature engineering workflow
* Automated operational filtering
* Export optimized reproducible architecture

---

## Downstream Dependencies

Notebook 2 produces the primary datasets required by:

* Notebook 3 predictive modeling workflows
* Notebook 4 clustering and hotspot analysis workflows

The outputs generated here serve as the analytical backbone for all downstream operational intelligence tasks.

---

## Recommended Use Cases

* Predictive operational analytics
* Delay risk modeling
* Service request conditioning
* Feature engineering pipelines
* Operational recurrence analysis
* Municipal workload preparation for machine learning

---

# Notebook 3 v3

# Core Modeling for Delay Risk and Resolution Time

## Overview

Notebook 3 performs predictive modeling focused on operational delay risk classification and response time regression analysis.

The notebook evaluates machine learning models designed to identify high risk service request environments before significant operational backlog escalation occurs.

The notebook supports both classification and regression workflows and produces management ready predictive summaries for operational planning.

---

## Primary Objectives

* Predict elevated delay risk conditions
* Predict operational response time behavior
* Evaluate classification model performance
* Evaluate regression model performance
* Generate interpretable operational feature importance
* Produce threshold optimization analysis
* Support predictive staffing and operational planning

---

## Core Workflow

### 1. Modeling Dataset Loading

The notebook loads the conditioned modeling dataset generated by Notebook 2.

The workflow uses:

* Preconditioned operational records
* Engineered timing metrics
* Repeat complaint proxy features
* Operational categorical variables
* Geographic and workload indicators

---

### 2. Preprocessing Pipeline

The notebook applies preprocessing workflows including:

* Feature encoding
* Numerical scaling
* Train test splitting
* Pipeline based preprocessing architecture
* Missing value handling

The preprocessing structure supports reproducible model experimentation and consistent evaluation.

---

### 3. Delay Risk Classification

Classification models are trained to predict elevated operational delay conditions.

The notebook evaluates multiple machine learning approaches and compares:

* ROC AUC performance
* Precision recall behavior
* Threshold tradeoffs
* Confusion matrix distributions
* Operational sensitivity behavior

The classification workflow supports proactive operational intervention planning.

---

### 4. Threshold Optimization

The notebook generates threshold tuning analysis to evaluate operational tradeoffs between:

* Precision
* Recall
* False positive risk
* False negative risk
* Operational intervention sensitivity

Threshold tuning is particularly important in municipal operational environments where staffing constraints and intervention costs must be balanced carefully.

---

### 5. Response Time Regression

Regression models are trained to estimate operational response time behavior.

Regression evaluation includes:

* Predicted versus actual comparisons
* Error evaluation metrics
* Model comparison summaries
* Operational timing estimation analysis

---

### 6. Feature Importance and Interpretability

Interpretable feature importance outputs are generated for operational analysis.

These outputs help identify:

* Strong operational delay drivers
* Geographic operational patterns
* Repeat complaint effects
* High impact operational features

Interpretability outputs support management decision making and operational transparency.

---

## Key Outputs

### Classification Outputs

| Output File                                         | Description                              |
| --------------------------------------------------- | ---------------------------------------- |
| `classification_metrics_delay_risk_48h.csv`         | Classification model performance metrics |
| `classification_threshold_curve_delay_risk_48h.csv` | Threshold tuning analysis                |
| `threshold_tradeoff_delay_risk_48h.png`             | Precision recall tradeoff visualization  |
| `confusion_matrix_{name}.png`                       | Confusion matrices for evaluated models  |
| `roc_curve_{best_class_model_name}.png`             | ROC performance visualization            |
| `pr_curve_{best_class_model_name}.png`              | Precision recall visualization           |

---

### Regression Outputs

| Output File                               | Description                         |
| ----------------------------------------- | ----------------------------------- |
| `regression_metrics_response_time.csv`    | Regression evaluation metrics       |
| `predicted_vs_actual_{best_reg_name}.png` | Regression prediction visualization |

---

### Interpretability Outputs

| Output File                                   | Description                            |
| --------------------------------------------- | -------------------------------------- |
| `top_logistic_coefficients_delay_risk.csv`    | Logistic regression feature importance |
| `top_random_forest_importance_delay_risk.csv` | Random forest feature importance       |
| `report_ready_modeling_findings.csv`          | Executive ready modeling summary       |
| `notebook3_v3_manifest.json`                  | Notebook execution metadata            |

---

## Operational Value

Notebook 3 provides predictive operational intelligence designed to support proactive municipal service management.

Key operational applications include:

* Predictive staffing allocation
* Delay risk escalation monitoring
* Early backlog intervention
* High risk operational prioritization
* Workload forecasting support
* Resource optimization planning

The classification models allow operational teams to identify elevated delay environments before backlog conditions become operationally severe.

The regression workflows support workload timing estimation and operational scheduling analysis.

---

## Technical Highlights

* End to end preprocessing pipelines
* Multi model evaluation framework
* Threshold optimization analysis
* Interpretable feature importance generation
* Classification and regression integration
* Export oriented reporting workflow
* Reproducible machine learning architecture

---

## Recommended Use Cases

* Delay risk prediction
* Backlog escalation forecasting
* Municipal staffing optimization
* Operational SLA monitoring
* Predictive service management
* Resource prioritization workflows

---

# Notebook 4 v3

# Operational Clustering, Hotspots, and Trend Analysis

## Overview

Notebook 4 performs unsupervised operational clustering, geographic hotspot analysis, and temporal trend analysis using the conditioned datasets generated by Notebook 2.

The notebook identifies operational workload environments, recurring geographic concentration patterns, and evolving service request trends across municipal operational units.

The notebook functions as the strategic operational intelligence layer of the pipeline.

---

## Primary Objectives

* Identify operational workload segments
* Detect geographic hotspot concentration
* Analyze operational clustering behavior
* Evaluate temporal operational trends
* Support workload segmentation analysis
* Generate management ready operational intelligence
* Identify recurring operational environments

---

## Core Workflow

### 1. Conditioned Dataset Loading

The notebook loads the conditioned analytical datasets produced by Notebook 2.

The workflow uses:

* Operational timing metrics
* Complaint concentration indicators
* Geographic variables
* Repeat complaint proxies
* Operational workload summaries

---

### 2. Operational Unit Aggregation

Operational records are aggregated into operational units for clustering analysis.

Aggregation metrics include:

* Complaint volume
* Average response time
* Repeat complaint indicators
* Geographic workload concentration
* Operational timing behavior

---

### 3. K Means Clustering

The notebook applies K Means clustering to identify operational workload segments.

The clustering workflow includes:

* Silhouette based cluster selection
* PCA dimensionality reduction
* Operational segment profiling
* Segment visualization

The resulting operational segments help identify:

* High workload operational environments
* High delay operational environments
* Stable operational regions
* Recurring workload concentration environments

---

### 4. PCA Operational Visualization

Principal Component Analysis is used to visualize operational segment separation.

The PCA outputs support:

* Operational interpretability
* Segment comparison
* Cluster quality assessment
* Executive reporting visualizations

---

### 5. Geographic Hotspot Analysis

The notebook identifies recurring operational hotspot environments across boroughs and operational units.

Hotspot analysis supports:

* Workload concentration analysis
* Geographic staffing optimization
* Recurring operational risk identification
* High burden operational region detection

---

### 6. Temporal Trend Analysis

The notebook evaluates operational behavior over time using monthly trend analysis.

Trend analysis helps identify:

* Seasonal operational shifts
* Emerging complaint environments
* Persistent workload escalation patterns
* Operational growth trends

---

## Key Outputs

### Clustering Outputs

\* Not stored in the repository due to size limit
| Output File                                         | Description                                         |
| --------------------------------------------------- | --------------------------------------------------- |
| `operational_segment_profile.csv`                   | Operational cluster summary statistics              |
| `operational_units_with_segments.csv`               | Operational units with assigned segments            |
| `management_ready_clustering_findings.csv`          | Executive ready clustering summary                  |
| `k_selection_silhouette.csv`                        | Silhouette analysis metrics                         |
| `*model_sample_with_operational_segments_v3.parquet`| Modeling dataset enriched with operational segments |

---

### Visualization Outputs

| Visualization                   | Purpose                                        |
| ------------------------------- | ---------------------------------------------- |
| `k_selection_silhouette.png`    | Cluster selection evaluation                   |
| `operational_segments_pca.png`  | PCA operational cluster visualization          |
| `segment_volume.png`            | Segment workload comparison                    |
| `segment_avg_response_time.png` | Segment timing comparison                      |
| `monthly_volume_by_segment.png` | Temporal workload trends                       |
| `top_geographic_hotspots.png`   | Geographic hotspot concentration visualization |

---

### Geographic and Trend Outputs

| Output File                                | Description                              |
| ------------------------------------------ | ---------------------------------------- |
| `geographic_hotspot_summary.csv`           | Geographic hotspot operational summary   |
| `monthly_trend_by_operational_segment.csv` | Monthly operational trend summary        |
| `top_operational_units_by_segment.csv`     | Highest concentration operational units  |
| `operational_unit_summary_all.csv`         | Full operational aggregation summary     |
| `operational_unit_summary_modeling.csv`    | Modeling focused operational aggregation |
| `notebook4_v3_manifest.json`               | Notebook execution metadata              |

---

## Operational Value

Notebook 4 provides strategic operational intelligence capable of supporting long term municipal planning and proactive resource management.

Major operational applications include:

* Geographic staffing optimization
* Operational hotspot escalation management
* Seasonal workload preparation
* Long term infrastructure prioritization
* Repeat complaint environment identification
* Borough level operational planning
* Predictive workload balancing

The hotspot analysis is particularly valuable for identifying recurring high burden operational environments that may require proactive intervention instead of reactive complaint resolution.

The clustering outputs also support segmentation based operational management strategies rather than one size fits all operational policies.

---

## Technical Highlights

* Unsupervised clustering workflows
* Silhouette based cluster optimization
* PCA dimensionality reduction
* Geographic hotspot analytics
* Temporal trend analysis
* Management oriented segmentation outputs
* Export optimized operational reporting

---

## Recommended Use Cases

* Operational segmentation
* Municipal hotspot analysis
* Geographic workload planning
* Seasonal operational forecasting
* Strategic service optimization
* Resource allocation planning
* Long term operational intelligence

---

# Repository Level Notes

## Pipeline Architecture

The notebooks are designed to run sequentially:

| Notebook   | Purpose                                      |
| ---------- | -------------------------------------------- |
| Notebook 1 | Intake profiling and representative sampling |
| Notebook 2 | Conditioning and feature engineering         |
| Notebook 3 | Predictive modeling                          |
| Notebook 4 | Clustering and operational intelligence      |

---

## Analytical Themes

The pipeline focuses heavily on:

* Delay risk prediction
* Operational workload concentration
* Geographic hotspot analysis
* Repeat complaint behavior
* Response time analysis
* Predictive operational management
* Scalable municipal analytics

---

## Typical Operational Questions Addressed

* Which complaint environments are most operationally severe?
* Which operational regions experience recurring workload concentration?
* Which requests are most likely to experience elevated delay risk?
* Where should staffing resources be prioritized?
* Which boroughs demonstrate persistent operational burden?
* How can predictive analytics support backlog reduction?
* Which operational environments require proactive intervention?

---

## Suggested Repository Structure

```text
project_root/
│
├── notebook_1_v3_full_dataset_intake_profiling.ipynb
├── notebook_2_v3_conditioning_representative_sampling.ipynb
├── notebook_3_v3_delay_risk_modeling.ipynb
├── notebook_4_v3_operational_clustering_trends.ipynb
│
├── notebook1_v3_outputs/
├── notebook2_v3_outputs/
├── notebook3_v3_outputs/
├── notebook4_v3_outputs/
│
└── README.md
```

---

## Recommended Libraries

Typical dependencies include:

* pandas
* numpy
* pyarrow
* scikit learn
* matplotlib
* seaborn
* scipy
* json
* zipfile

---

## Final Notes

This project demonstrates a complete operational analytics workflow capable of supporting large scale municipal service optimization.

The pipeline combines:

* Large scale data engineering
* Operational profiling
* Predictive machine learning
* Geographic hotspot analysis
* Unsupervised segmentation
* Trend analysis
* Management oriented operational intelligence

The workflow was designed to balance analytical rigor, operational interpretability, scalability, and management usability within a high volume municipal service environment.

