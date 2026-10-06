# COVID-19 Data Pipeline & Analytics Dashboard

## Project Overview

This project implements an end-to-end COVID-19 data pipeline using Python, PostgreSQL, Google Sheets, and Looker Studio.

The pipeline retrieves Johns Hopkins COVID-19 daily report data from GitHub, standardizes and transforms the historical files into analytical datasets, stores processed outputs in PostgreSQL and CSV format, and presents the results through an interactive Looker Studio dashboard.

## Architecture

GitHub COVID-19 Repository  
↓  
GitHub API  
↓  
Python / Pandas  
↓  
Data Cleaning & Transformation  
↓  
Processed CSV Outputs  
↓  
PostgreSQL Analytical Database  
↓  
Google Sheets Reporting Layer  
↓  
Looker Studio Dashboard  

## Data Source

Source repository:

Johns Hopkins CSSE COVID-19 dataset

Daily reports were discovered programmatically through the GitHub repository structure.

### Source coverage

- Total daily CSV files processed: 1,143
- Date range: 22 January 2020 to 9 March 2023

## Data Pipeline

The Python pipeline performs the following steps:

1. Connects to the GitHub repository.
2. Discovers dated COVID-19 daily report CSV files.
3. Reads all valid daily reports.
4. Standardizes historical schema differences.
5. Converts relevant measures to numeric data types.
6. Standardizes selected country naming differences.
7. Aggregates province/state-level records to country level.
8. Combines all reports into a country-day analytical dataset.
9. Checks duplicate country-date records.
10. Creates analytical metrics.
11. Generates data-quality checks.
12. Saves processed CSV outputs.
13. Loads curated datasets into PostgreSQL.

## Analytical Grain

The main curated dataset uses:

**One row per country per reporting date**

This structure supports country-level time-series analysis and dashboard filtering.

## Calculated Metrics

The pipeline creates analytical fields including:

- Confirmed Cases
- Deaths
- Recovered Cases
- New Cases
- New Deaths
- Adjusted New Cases
- Adjusted New Deaths
- Case Fatality Rate

### Case Fatality Rate

Case Fatality Rate is calculated as:

Deaths / Confirmed Cases × 100

## Processed Outputs

### covid_country_daily.csv

Main country-day analytical dataset used for country-level analysis.

### global_daily_kpis.csv

Daily global COVID-19 totals and derived metrics.

### latest_country_snapshot.csv

Latest available country-level snapshot for ranking and comparison.

### data_quality_report.csv

Summary of data-quality checks including:

- Row counts
- Country coverage
- Date coverage
- Duplicate checks
- Missing values
- Failed source files

## PostgreSQL Tables

The following analytical tables are loaded into PostgreSQL:

- covid_country_daily
- global_daily_kpis
- latest_country_snapshot
- data_quality_report

## Dashboard

The Looker Studio report contains three analytical pages:

### Global COVID-19 Overview

Includes:

- Total Confirmed Cases
- Total Deaths
- Global Case Fatality Rate
- Global cumulative trends
- Daily global trends

### Country Daily Analysis

Includes:

- Country filter
- Date filter
- Confirmed cases trend
- Death trend
- Daily new cases
- Daily new deaths
- Case fatality rate trend

### Latest Country Snapshot

Includes:

- Countries covered
- Latest confirmed totals
- Latest deaths
- Top countries by confirmed cases
- Top countries by deaths
- Country comparison table
- Geographic comparison

## Technologies

- Python
- Pandas
- NumPy
- Requests
- PostgreSQL
- SQLAlchemy
- psycopg2
- Google Sheets
- Looker Studio
- GitHub

## Project Structure

```text
COVID_Data_Pipeline/
├── notebooks/
│   └── covid_pipeline.ipynb
├── data/
│   └── processed/
│       ├── covid_country_daily.csv
│       ├── global_daily_kpis.csv
│       ├── latest_country_snapshot.csv
│       └── data_quality_report.csv
├── dashboard/
├── README.md
├── requirements.txt
└── .gitignore