---
title: "RHoMIS Food Security Analytics"
date: 2026-04-28
description: "End-to-end analysis of 54,873 smallholder farm households across 35 countries. ETL pipeline, statistical modelling, and interactive Tableau dashboard."
image: /images/projects/rhomis-banner.jpg
badges:
  - "Python"
  - "Pandas"
  - "Tableau"
  - "scikit-learn"
  - "SciPy"
  - "k-means"
  - "ETL Pipeline"
  - "EDA"
  - "Statistical Testing"
links:
  - icon: fab fa-github
    url: https://github.com/mahir-m01/Section-C_G-7_RHoMIS-Analytics
featured:
  name: "Tableau Dashboard"
  link: https://public.tableau.com/app/profile/rajdeep.sanyal/viz/RHoMISDASHBOARD/INCOMEPOSITION
showInHome: false
toc: true
tags:
  - DVA
  - Tableau
  - Python
  - Statistical Analysis
---

{{< rawhtml >}}
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:2rem;">
  <a href="https://github.com/mahir-m01/Section-C_G-7_RHoMIS-Analytics" target="_blank" style="display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:6px;background:#21262d;color:#e4e6eb;text-decoration:none;font-size:0.875rem;border:1px solid #30363d;">
    <i class="fab fa-github"></i> GitHub
  </a>
  <a href="https://public.tableau.com/app/profile/rajdeep.sanyal/viz/RHoMISDASHBOARD/INCOMEPOSITION" target="_blank" style="display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:6px;background:#21262d;color:#4fc3f7;text-decoration:none;font-size:0.875rem;border:1px solid #30363d;">
    <i class="fas fa-chart-bar"></i> Tableau Dashboard
  </a>
  <a href="https://dataverse.harvard.edu/dataset.xhtml?persistentId=doi%3A10.7910%2FDVN%2FWS38SA" target="_blank" style="display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:6px;background:#21262d;color:#e4e6eb;text-decoration:none;font-size:0.875rem;border:1px solid #30363d;">
    <i class="fas fa-database"></i> Dataset
  </a>
</div>
{{< /rawhtml >}}

## Overview

This project analyses structural food insecurity across smallholder farming households in 35 countries using the RHoMIS (Rural Household Multi-Indicator Survey) dataset published on Harvard Dataverse. The dataset spans surveys conducted between 2015 and 2023, covering 54,873 households across Sub-Saharan Africa, Latin America, and Asia.

The goal was to identify which regions and farm profiles are most vulnerable to food insecurity and low income, and what structural factors drive these outcomes — to provide a data-driven basis for targeting development interventions.

---

## Dataset

The raw dataset contained 1,599 survey variables across 54,873 records. Through a 5-stage ETL pipeline, this was reduced to 46 Tableau-ready analytical features covering:

- **Identity and geography**: country, ISO code, GPS coordinates, survey year
- **Demographics**: household size, age distribution, gender of household head, education level
- **Farm and land**: cultivated area, land tenure, irrigation access, labour type
- **Crop production**: harvest volumes, crop income, consumption proportions
- **Income**: off-farm income share, livestock sales, income quintile rank
- **Food security**: food shortage duration, FIES and HFIAS indices

No imputation was applied. Missing values were preserved as `NaN` throughout. Missingness in RHoMIS is structural and reflects survey design, not data error.

---

## Pipeline Architecture

The analytical pipeline ran across five stages:

1. **Extraction**: Load, validate schema, select 60 working columns from 1,599
2. **Cleaning**: Structural normalisation, unit conversion, derived field construction
3. **EDA**: Distribution analysis, geographic breakdown, gender disaggregation
4. **Statistical Analysis**: Hypothesis testing, regression, clustering
5. **Load Preparation**: KPI derivation, Tableau-ready CSV export

---

## KPI Framework

Seven KPIs formed the backbone of the dashboard, each tied directly to a policy recommendation:

| KPI | Value |
|---|---|
| Food Shortage Rate | 67.7% |
| Affected Households | 32,097 of 47,399 |
| Median Shortage Duration | 3.0 months |
| Irrigation Access Rate | 20.2% |
| Median Land Productivity | 600 kg/ha |
| Median Income per MAE | $112 PPP |
| Shortage Rate (Lowest Quintile) | 75.8% |

---

## Statistical Methods

**Logistic Regression** (with country fixed effects) identified income rank as the strongest predictor of food shortage (OR 0.456, p < 0.001). Low education (OR 0.71) and large household size compounded every other risk factor.

**Mann-Whitney U Tests** confirmed statistically significant differences in land productivity and income between irrigated and rainfed households (p < 0.001).

**Chi-Square Tests** validated associations between gender of household head and food shortage rates, resource control patterns, and off-farm income participation.

**K-Means Clustering** (k=6, standardised features) produced six distinct vulnerability profiles. The low-income rainfed cluster (14,330 households) had a 78.7% food shortage rate and 0.3% irrigation coverage, making it the single highest-return intervention target.

---

## Key Findings

- **67.7% of households reported food shortage** — this is the structural norm, not an exception
- **Irrigation gap is the clearest addressable lever**: irrigated households face 55.1% shortage vs 72.4% rainfed, a 17.4 percentage point difference, yet only 20.2% of households have irrigation access
- **Land productivity quartile creates a 29.1pp spread**: Q1 households face 83% shortage, Q4 face 54%
- **Country-level spread reaches 84pp**: DRC (90.7%) and Comoros (87.0%) anchor the high end; India (10.5%) and Costa Rica (18.6%) the low end
- **Female-headed households face a consistent additional penalty** across shortage rates and resource control (chi-square p < 0.001)

---

## Tableau Dashboard

{{< rawhtml >}}
<img src="/images/projects/rhomis-dashboard.png" alt="RHoMIS Tableau Dashboard — Risk Overview" style="width:100%;border-radius:8px;margin-bottom:1.5rem;border:1px solid #30363d;">
{{< /rawhtml >}}

The dashboard was published on Tableau Public with four interactive views:

- **Risk Overview**: choropleth map, food shortage rate by country, median months of shortage
- **Vulnerability Profiles**: shortage by k-means cluster across countries, demographic heatmap
- **Structural Drivers**: productivity quartile vs irrigation, crop diversity, land scatter
- **Income Position**: income rank vs food shortage, off-farm income by profile, quintile distribution

All views support cross-filtering by country, year, irrigation flag, vulnerability profile, and gender.

---

## Tech Stack

Python, Pandas, NumPy, Statsmodels, scikit-learn, Matplotlib, Seaborn, Tableau Public, Jupyter Notebooks, Git
