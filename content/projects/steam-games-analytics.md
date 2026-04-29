---
title: "Steam Games Market Analytics"
date: 2026-02-28
description: "Market structure analysis of ~7,000 Steam titles. KPI engineering, pricing dynamics, and an interactive Google Sheets dashboard."
image: /images/projects/steam-logo.png
badges:
  - "Google Sheets"
  - "KPI Design"
  - "Pivot Tables"
  - "EDA"
  - "Dashboard Design"
  - "Market Analysis"
links:
  - icon: fab fa-github
    url: https://github.com/mahir-m01/SectionC_Group2_SteamGames
featured:
  name: "GitHub Repository"
  link: https://github.com/mahir-m01/SectionC_Group2_SteamGames
showInHome: false
toc: true
tags:
  - DVA
  - Dashboard
  - Market Analysis
  - Google Sheets
---

{{< rawhtml >}}
<div style="display:flex;gap:12px;flex-wrap:wrap;margin-bottom:2rem;">
  <a href="https://github.com/mahir-m01/SectionC_Group2_SteamGames" target="_blank" class="project-button" style="display:inline-flex;align-items:center;gap:6px;padding:8px 16px;border-radius:6px;background:#21262d;color:#e4e6eb;text-decoration:none;font-size:0.875rem;border:1px solid #30363d;">
    <i class="fab fa-github"></i> GitHub
  </a>
</div>
{{< /rawhtml >}}

## Overview

This project examines how pricing models, content structure, platform accessibility, and user feedback influence game popularity and player engagement on the Steam marketplace. The analysis covers approximately 7,000 titles sampled from a raw dataset of over 50,000 games, filtered by descending Peak Concurrent Users (CCU) to focus on commercially active titles.

The objective was to identify the structural drivers of engagement and quantify where market concentration lies within the catalogue.

---

## Dataset

- **Source**: Kaggle (public Steam metadata)
- **Original size**: ~50,000 games
- **Analysis sample**: ~7,000 titles (sampled by Peak CCU)
- **Key fields**: price, discount percentage, positive/negative reviews, Peak CCU, genres, platforms supported, DLC count, average playtime, release date

All cleaning and preparation was performed in Google Sheets. Steps included removing non-analytical metadata columns, standardising data types (dates, currency, percentages), converting array-based fields (genres, platforms, languages) into count metrics, normalising platform indicators to boolean format, and filling sparse playtime values with column averages where required.

---

## Feature Engineering

Analytical columns derived to support KPI calculation and segmentation:

| Feature | Definition |
|---|---|
| Total Reviews | Positive + Negative review count |
| Weighted Sentiment Score | `% Positive × ln(Total Reviews + 1)` |
| Pricing Type | Free-to-Play / Paid classification |
| Platform Count | Sum of Windows + Mac + Linux support |
| Popularity Tier | Niche / Rising / Popular / Blockbuster (Peak CCU thresholds) |
| Discount Impact | Discount % × Peak CCU |
| Price Band | Bucketed price ranges |
| DLC Band | Bucketed DLC count ranges |
| Recommendation Band | Bucketed review volume ranges |

---

## Key Findings

- **Free-to-Play titles generate 5.7x higher average Peak CCU than Paid**: the engagement advantage of zero price point is consistent across genres and content depth
- **93% of the Steam catalogue falls into the Niche tier**: a small number of Blockbuster titles capture a disproportionate share of total concurrent player activity
- **Higher recommendation volume strongly correlates with Peak CCU**: organic discovery compounds early engagement advantages
- **Multi-genre, content-rich games achieve higher concurrency**: DLC count and genre breadth are positively associated with player retention
- **Higher-priced games show stronger Weighted Sentiment**: paid audiences tend to be more selective, resulting in higher review quality at lower volume

---

## Dashboard

{{< rawhtml >}}
<img src="/images/projects/steam-dashboard.png" alt="Steam Games Dashboard" style="width:100%;border-radius:8px;margin-bottom:1.5rem;border:1px solid #30363d;">
{{< /rawhtml >}}

The final dashboard was built in Google Sheets with a dark theme styled after the Steam desktop interface. It includes:

- KPI cards for engagement, satisfaction, market structure, and discovery metrics
- 15+ pivot tables covering pricing type, popularity tier, content depth, and social proof segmentation
- Dynamic slicers for interactive filtering across pricing, genre count, popularity tier, DLC band, and recommendation band
- Navigation buttons for smooth movement between analysis sections

---

## Tech Stack

Google Sheets (Advanced), Pivot Tables, Conditional Formatting, KPI Design, Exploratory Data Analysis, Git, GitHub
