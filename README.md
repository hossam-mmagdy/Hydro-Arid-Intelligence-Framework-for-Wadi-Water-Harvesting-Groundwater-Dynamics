# Hydro-Arid Intelligence Framework for Wadi Water Harvesting & Groundwater Dynamics

## Abstract

This repository presents an integrated computational framework for quantitative assessment of water resource dynamics in hyper-arid coastal desert environments. The system synthesizes hydraulic process modeling, geospatial terrain analysis, and machine learning ensemble methods to optimize ephemeral river (wadi) water harvesting infrastructure and predict groundwater system behavior under anthropogenic and climatic forcing scenarios.

## 1. System Architecture

### 1.1 Core Computational Modules

| Module | Scientific Methodology | Application Domain |
|--------|------------------------|-------------------|
| Climate Data Generator | Stochastic autoregressive modeling with IPCC-compliant climate trend forcing | 45-year monthly time series reconstruction (1980-2024) |
| Hydraulic Modeling System | Manning-Strickler flow resistance, Froude-critical depth analysis, D8 flow routing algorithm | Flood wave propagation and retention basin design |
| Check Dam Optimizer | Multi-criteria suitability analysis with spatial autocorrelation constraints | Strategic infrastructure placement in channel networks |
| Flood Simulation Engine | 2D diffusive wave approximation with explicit finite-difference scheme | Event-based inundation mapping and volume quantification |
| AI Prediction System | Ensemble learning (Random Forest, Gradient Boosting, MLP, SVR) with temporal feature engineering | Groundwater level and salinity forecasting |

### 1.2 Study Domain

**Geographic Extent:** Marsa Matrouh, Northwestern Egypt (31.3525°N, 27.2373°E)  
**Köppen-Geiger Classification:** BWh (Hot Desert Climate)  
**Mean Annual Precipitation:** 145 mm (decreasing trend: -0.6 mm/yr)  
**Mean Annual Temperature:** 20.5°C (increasing trend: +0.18°C/decade)  
**Aridity Index:** 0.08 (hyper-arid)

## 2. Methodological Framework

### 2.1 Hydrological Process Representation

The climatic data generation employs physically-based parameterization:
T_monthly = T_base + T_trend·t + A_T·sin(2πt/12 - π/2) + ε_T(σ_T)
P_monthly = P_annual·α_seasonal + ε_P(σ_P)
ET_monthly = ET_base + A_ET·sin(2πt/12) + ET_trend·t + ε_ET
plain
Copy

Where ε represents Gaussian noise terms with time-dependent variance accounting for increasing climate variability.

### 2.2 Groundwater System Dynamics

Aquifer response follows the water balance formulation:
Δh/Δt = (R - ET_loss - Q_abstraction + Q_intrusion) / S_y
R = α_recharge · P
ET_loss = β_et · ET_potential
Q_intrusion = max(0, (h - h_sea)·k_intrusion)
plain
Copy

With specific yield S_y = 0.15, recharge coefficient α = 0.15, and sea intrusion threshold h_sea = 30 m.

### 2.3 Machine Learning Implementation

Feature engineering incorporates:

- **Temporal lags:** 1-12 month lookback windows
- **Rolling statistics:** 6-month moving mean and standard deviation
- **Cyclical encoding:** Sinusoidal month representation (sin/cos)
- **Derived indices:** Aridity index, water stress index, Standardized Precipitation Index (SPI)

Model validation employs 80/20 temporal split with R², RMSE, and MAE metrics.

## 3. Repository Structure
├── data/
│   └── marsa_matrouh_scientific_data.csv    # Synthesized climatological and hydrogeological records
├── terrain/
│   └── terrain_data.npz                     # Digital elevation model and simulation outputs
├── src/
│   ├── data_generator.py                    # Climate and groundwater data synthesis classes
│   ├── hydraulic_modeling.py                # Flow routing and dam optimization algorithms
│   ├── flood_simulation.py                  # 2D flood propagation engine
│   └── ai_prediction.py                     # Ensemble machine learning implementation
├── notebooks/
│   └── hydro_arid_framework.ipynb           # Executable demonstration workflow
└── README.md
