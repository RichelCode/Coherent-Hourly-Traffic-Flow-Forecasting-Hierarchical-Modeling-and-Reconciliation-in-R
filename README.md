# Coherent Hourly Traffic Flow Forecasting: A Reduced-Scale Hierarchical Reconciliation Study in R

## Overview

This repository contains a complete R-based project on hierarchical time series forecasting and forecast reconciliation using hourly traffic flow data. The project was developed as an academic forecasting study and structured to meet graduate-level standards of rigor, reproducibility, and clarity.

To make the workflow computationally feasible, the analysis uses a reduced-scale but structurally rich subset of the original dataset. Rather than modeling the full traffic archive, this project focuses on **November 2024** and retains a deterministic subset of complete station-level series. This keeps the project practical to run while preserving the essential features of hierarchical forecasting.

The core objective is to compare alternative reconciliation strategies for producing **coherent forecasts** across a traffic hierarchy that runs from individual stations to total system flow.

## Research question

How do alternative forecast reconciliation methods affect forecast accuracy across different levels of an hourly traffic hierarchy in a reduced one-month traffic sample, and how robust are those conclusions to forecast horizon?

## Main contributions

This repository provides:

- a computationally efficient reduced-scale hierarchical forecasting design,
- a strict and interpretable traffic hierarchy,
- a deterministic station-selection procedure for reproducibility,
- competing univariate base forecasting models,
- multiple reconciliation strategies,
- level-wise forecast evaluation,
- formal theoretical discussion,
- robustness checks across forecast horizons.

## Reduced-scale study design

The full dataset was too large for efficient end-to-end estimation across all models and reconciliation methods. To address this, the project uses only **November 2024**, which still provides:

- **720 hourly observations** per complete series,
- **more than 100 bottom-level series**,
- a clear additive aggregation structure,
- enough temporal depth for short-horizon forecasting and reconciliation analysis.

Within November 2024, the analysis keeps only stations with complete observations for the full month. Then, within each `Route × Direction × Lane Type` cell, it retains up to **three stations**, selected deterministically by station identifier. This preserves structural diversity while keeping runtime manageable.

## Data

The analysis uses an hourly traffic flow dataset with the following key fields:

- `Timestamp`
- `Route`
- `Direction of Travel`
- `Lane Type`
- `Station`
- `Total Flow`

The target variable is `Total Flow`. The remaining variables define the cross-sectional aggregation structure.

For this reduced-scale version of the project, the working sample is restricted to:

- **November 2024 only**,
- stations with complete hourly observations for that month,
- a deterministic subset of up to three stations per `Route × Direction × Lane Type` group.

## Main hierarchy

The primary hierarchy is:

**Total -> Route -> Route-Direction -> Route-Direction-Lane Type -> Station**

This specification supports bottom-up, top-down, and MinT reconciliation in the main analysis.

## Leakage-control strategy

This project uses a strict time-series evaluation design:

1. the data are split **chronologically**, not randomly,
2. the training period contains earlier observations,
3. the test period contains later observations,
4. the final **7 days of November 2024** are reserved as the holdout set,
5. only complete station series are used, so **no imputation is performed**,
6. test outcomes remain untouched until final evaluation.

This design keeps the forecasting workflow clean, reproducible, and appropriate for time series analysis.

## Methods

### Base models
- ETS
- ARIMA

### Reconciliation methods
- Bottom-up
- Top-down using forecast proportions
- Top-down using historical proportions
- MinT with shrinkage covariance
- MinT with sample covariance

### Accuracy measures
- RMSE
- MAE
- MASE
- RMSSE

### Robustness checks
- Alternative forecast horizons: 24, 72, and 168 hours
- Optional grouped/cross-classified extension
