NLP-Based Complaint Categorization

Unstructured NYC 311 complaint text was transformed into structured, actionable categories using a two-step NLP approach.

Approach

A representative sample was used to:

Clean and combine key text fields
Generate semantic embeddings
Cluster similar complaints

These clusters were then reviewed and consolidated into business-relevant categories, including:

Heating
Noise
Parking
Sanitation
Infrastructure
Full Dataset Application

The learned patterns were applied to the full dataset using batch processing. Each record was assigned an issue category, resulting in an enriched dataset.

A summary of category volume and distribution is available in:

full_issue_category_counts.csv
Provides total counts and percentage share by category
Highlights the relative distribution of issue types across all records
Validation and Preview

To validate the transformation, a stratified sample of the enriched dataset was generated:

sample_issue_category_preview.csv
Includes original complaint fields alongside assigned categories
Demonstrates consistent grouping of similar issues
Preserves record-level detail for review
Outcome

This process converts raw, unstructured text into a scalable and interpretable feature. The resulting dataset supports:

Analysis of complaint trends
Service demand insights
Operational performance evaluation
