# Renewable Energy Adoption — Data Modelling & Interactive Dashboard

An end-to-end business-intelligence project that models multidimensional renewable-energy data and presents it through an interactive Tableau dashboard. The work covers the full BI lifecycle: dimensional modelling (star schema), purpose-built data marts, and a coordinated, interactive dashboard designed for a policy-maker audience.

> **Live dashboard:** [View on Tableau Public](ADD_YOUR_TABLEAU_PUBLIC_LINK_HERE)
> *(Best viewed in a desktop browser — the dashboard is fully interactive, with filters and cross-highlighting.)*

---

## Overview

The dataset tracks renewable-energy adoption across multiple countries from 2010–2023, with metrics on energy production, investment, installed capacity, environmental impact, and job creation across five sources: solar, wind, hydro, geothermal, and biomass.

The project answers two core business questions:

1. **Total energy production by source, by geography** — which countries lead in renewable production, and how is their output composed across sources?
2. **Trends in energy production by year, by source** — how has each source's adoption changed over the 14-year period?

---

## Approach

### 1. Dimensional model (star schema)

The data was structured using a star schema, following a four-step dimensional design:

- **Business process:** analysing renewable-energy adoption metrics
- **Grain:** one record per country, per year, per energy source
- **Dimensions:** `Dim_Date`, `Dim_Location`, `Dim_EnergySource`, `Dim_Policy`
- **Facts:** numerical measures such as `Energy_Production_MWh`, `Investment_USD`, `Installed_Capacity_MW`, `CO2_Reduction_Tons`, and `Jobs_Created`, all additive across the dimensions

This structure keeps the fact table lean and numerical while pushing descriptive context into conformed dimensions, enabling fast aggregation along any combination of time, geography, and source.

### 2. Purpose-built data marts

Two data marts were designed, each optimised for one of the business questions:

- **`Production_by_Geography_Mart`** — joins the fact table to `Dim_Location` and `Dim_EnergySource`, deliberately excluding the time and policy dimensions to optimise for spatial/categorical aggregation. Powers the geographical comparison view.
- **`Production_Trends_Mart`** — joins the fact table to `Dim_Date` and `Dim_EnergySource`, excluding geography to focus on temporal patterns. Powers the time-series view.

Separating the two analytical concerns keeps each visualisation focused and performant.

### 3. Interactive dashboard

The dashboard combines two coordinated views:

- A **horizontal stacked bar chart** comparing total production across countries, with each segment showing a source's contribution — so leaders and their diversification strategies are visible at a glance.
- A set of **line charts** tracking each source's production over time, surfacing growth trajectories and decline.

Interactivity includes shared filters (country, year range, energy source) and a hover action that cross-highlights between the two views — hovering a country's bar filters the trend lines to that country, bridging spatial and temporal perspectives.

---

## Key findings

- **Solar and wind** showed the most consistent growth across countries over the period.
- **Hydroelectric** output declined in most countries, with Canada and Japan the main exceptions.
- The **USA** produced the most renewable energy in aggregate despite not leading any single category; **Japan** produced the least, partly due to low biomass adoption.
- Notable outliers included Germany's high hydro output, Brazil's high wind output, and Japan's and Germany's low biomass production.

---

## Repository contents

| File / folder | Description |
|---|---|
| `renewable-energy-dashboard.twbx` | Packaged Tableau workbook (includes data) |
| `/data` | Source dataset |
| `/images` | Dashboard screenshots and demo GIF used in this README |
| `README.md` | This file |

To open the workbook locally you'll need [Tableau Desktop](https://www.tableau.com/products/desktop) or the free [Tableau Public](https://public.tableau.com/) app. For a no-install view, use the live link above.

---

## Tools

Tableau (dimensional modelling, data marts, dashboard design) · star-schema design · interactive data visualisation

---

## Context

This project was completed as part of my BSc Computer Science studies at the University of Reading. It demonstrates dimensional data modelling and the design of interactive, audience-focused analytical tools — turning raw multidimensional data into a decision-support dashboard.
