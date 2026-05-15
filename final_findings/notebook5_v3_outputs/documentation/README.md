# Notebook 5 Management Resource Allocation Outputs

This folder contains management-facing outputs from Notebook 5.

## Purpose

The outputs convert NYC 311 analytical results into concrete operational metrics for leadership decision-making. These outputs support report sections about resource allocation, service delay pressure, hotspot recurrence, repeat complaint burden, and proactive operational planning.

## Key folders

- `tables/`: CSV outputs for report metrics and appendix tables.
- `plots/`: PNG charts suitable for insertion into the report or appendix.
- `documentation/`: Output inventory and run context.

## Most useful report tables

- `tables/borough_operational_kpi_stress_scores.csv`
- `tables/agency_operational_kpi_stress_scores.csv`
- `tables/complaint_type_operational_kpi_stress_scores.csv`
- `tables/borough_complaint_type_priority_matrix.csv`
- `tables/overall_sla_performance_summary.csv`
- `tables/borough_sla_performance_summary.csv`
- `tables/hotspot_resource_priority_rankings.csv`
- `tables/management_resource_priority_recommendations.csv`
- `tables/best_delay_risk_model_management_summary.csv`

## Most useful report plots

- `plots/borough_operational_stress_score.png`
- `plots/complaint_type_operational_stress_score_top15.png`
- `plots/agency_operational_stress_score_top15.png`
- `plots/hotspot_resource_priority_score_top15.png`
- `plots/pareto_complaint_type_workload_concentration.png`
- `plots/complaint_workload_vs_delay_rate_scatter.png`
- `plots/borough_complaint_delay_rate_heatmap.png`
- `plots/monthly_workload_trend_by_operational_segment.png`
- `plots/monthly_delay_rate_trend_by_operational_segment.png`

## Important interpretation note

This notebook does not claim to estimate actual staffing counts or budget requirements. It provides operational prioritization metrics based on workload, delay risk, response time, repeat complaint pressure, hotspot recurrence, and trend behavior.

## Input context

Notebook 1 full dataset rows noted in manifest: 20448149
Notebook 2 analysis-ready sample rows noted in manifest: 500000
Notebook 2 sample date range: 2020-01-01 00:04:47 to 2026-04-28 01:12:01
Notebook 4 unique months in sample: 76
