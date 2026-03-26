# Coherent Hourly Traffic Flow Forecasting: Hierarchical Modeling and Reconciliation in R

## Overview

This repository contains a complete R-based project on hierarchical time series forecasting and forecast reconciliation using hourly traffic flow data. The project was developed as an academic forecasting study and is structured to meet graduate-level standards of rigor, reproducibility, and clarity.

The core objective is to compare alternative reconciliation strategies for producing **coherent forecasts** across a traffic hierarchy that runs from individual stations to total system flow.

## Research question

How do alternative reconciliation methods affect forecast accuracy across different levels of an hourly traffic hierarchy, and how sensitive are those conclusions to forecast horizon and hierarchy specification?

## Main contributions

This repository provides:

- a leakage-safe forecasting workflow,
- a strict hierarchical traffic specification,
- competing univariate base models,
- multiple reconciliation strategies,
- level-wise forecast evaluation,
- formal theoretical discussion,
- robustness checks for horizon and structure.

## Data

The analysis uses an hourly traffic flow dataset with the following key fields:

- `Timestamp`
- `Route`
- `Direction of Travel`
- `Lane Type`
- `Station`
- `Total Flow`

The project treats `Total Flow` as the target variable and uses the remaining structural fields to define the aggregation system.

## Main hierarchy

The primary hierarchy is:

**Total -> Route -> Route-Direction -> Route-Direction-Lane Type -> Station**

This specification supports bottom-up, top-down, and MinT reconciliation.

## Leakage-control strategy

A major feature of this project is strict leakage prevention:

1. the forecast origin is set before imputation,
2. missing training values are imputed using training data only,
3. test targets are never imputed,
4. accuracy is computed only on genuinely observed holdout outcomes.

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
- Alternative forecast horizons
- Alternative grouped aggregation structure
