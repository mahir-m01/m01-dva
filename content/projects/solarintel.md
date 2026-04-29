---
title: "SolarIntel: Solar Energy Generation Prediction"
date: 2026-03-28
description: "End-to-end ML pipeline forecasting hourly solar output across 29 European countries, with a LangGraph agentic AI layer for grid-management recommendations."
image: /images/projects/nasa-banner.jpg
badges:
  - "Python"
  - "scikit-learn"
  - "Random Forest"
  - "LangGraph"
  - "LangChain"
  - "RAG"
  - "Streamlit"
  - "NASA POWER API"
  - "EMHIRES"
  - "Plotly"
links:
  - icon: fab fa-github
    url: https://github.com/mahir-m01/EMHIRES-NASA-SolarPrediction
featured:
  name: "Live Demo"
  link: https://huggingface.co/spaces/priyanshutomar2024/SolarIntel
showInHome: false
toc: true
tags:
  - Machine Learning
  - Agentic AI
  - Solar Energy
  - Streamlit
---

{{< rawhtml >}}
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:2rem;">
  <a href="https://github.com/mahir-m01/EMHIRES-NASA-SolarPrediction" target="_blank" class="project-button" style="display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:6px;background:#21262d;color:#e4e6eb;text-decoration:none;font-size:0.875rem;border:1px solid #30363d;">
    <i class="fab fa-github"></i> GitHub
  </a>
  <a href="https://huggingface.co/spaces/priyanshutomar2024/SolarIntel" target="_blank" class="project-button" style="display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:6px;background:#21262d;color:#4fc3f7;text-decoration:none;font-size:0.875rem;border:1px solid #30363d;">
    <i class="fas fa-external-link-alt"></i> Live Demo
  </a>
</div>
{{< /rawhtml >}}

## Overview

SolarIntel is an end-to-end machine learning and agentic AI system that forecasts hourly solar energy output across 29 European countries. The pipeline fuses 15 years of solar capacity factor data from the European Commission's EMHIRES dataset with hourly meteorological observations from the NASA POWER API, trains two regression models, and serves predictions through an interactive web application with an AI-powered grid advisory layer.

The system is deployed live on Hugging Face Spaces.

---

## Data Pipeline

**EMHIRES Dataset**: Solar PV capacity factor timeseries for 29 European countries from 2001 to 2015, published by the European Commission Joint Research Centre (Gonzalez Aparicio et al., 2017). Provides hourly generation normalised per unit of installed capacity.

**NASA POWER API**: Hourly meteorological data (solar irradiance, ambient temperature, wind speed) fetched for each country centroid across the same 15-year period.

**Merged Dataset**: 3.8 million rows, 34 features, covering all 29 countries at hourly resolution from 2001 to 2015. Features include capacity factor, irradiance components, temperature, wind speed, date-time decomposition (hour, month, season), and one-hot encoded country labels.

---

## Models

Two regression models were trained on an 80/20 train-test split (`random_state=67`):

| Metric | Linear Regression | Random Forest Regressor |
|---|---|---|
| MAE | 0.0534 | 0.0280 |
| RMSE | 0.0845 | 0.0547 |
| R² | 0.788 | **0.911** |

The Random Forest Regressor was selected as the production model. It was serialised with `joblib` and serves all real-time inference in the Streamlit application and agentic pipeline.

---

## Agentic AI Layer

A 4-node LangGraph pipeline sits on top of the ML model and provides structured grid-management recommendations based on forecasted generation profiles.

**Node 1 — Forecast**: Fetches live 24-hour weather data from the Open-Meteo API for the selected country, builds the feature vector, and runs inference through the Random Forest model to produce an hourly capacity factor profile.

**Node 2 — Risk Analysis**: Scores forecast variability and flags high-risk periods (e.g. hours with steep generation drops or sustained low output) with severity classifications: high, medium, or low.

**Node 3 — RAG Retrieval**: Queries a Chroma vector store populated with four grid management reference documents using local sentence-transformers embeddings. Retrieves contextually relevant passages to ground LLM recommendations.

**Node 4 — LLM Recommendations**: Passes the forecast summary, risk flags, and retrieved context to an LLM via OpenRouter. Returns structured JSON output with a forecast summary, risk period breakdown, and ranked grid strategies annotated with their retrieval source.

---

## Application Preview

{{< rawhtml >}}
<img src="/images/projects/solarintel-dashboard.png" alt="SolarIntel Streamlit Dashboard" style="width:100%;border-radius:8px;margin-bottom:1.5rem;border:1px solid #30363d;">
{{< /rawhtml >}}

## Web Application

The Streamlit application provides:

- **Real-time predictions**: select any of the 29 countries and generate an hourly solar output forecast
- **24-hour generation profile**: interactive Plotly chart of forecasted capacity factor
- **Feature importance**: Random Forest feature importance visualisation
- **Seasonal patterns**: historical generation profiles by season and country
- **Model performance**: MAE, RMSE, R² on the held-out test set
- **Agentic advisory**: trigger the LangGraph pipeline to receive structured grid recommendations

---

## Tech Stack

Python, Pandas, NumPy, scikit-learn, Matplotlib, Seaborn, Plotly, LangGraph, LangChain, RAG, Open-Meteo API, NASA POWER API, joblib, Hugging Face Spaces
