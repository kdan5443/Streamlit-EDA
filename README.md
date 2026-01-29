# Streamlit-EDA

**Interactive Exploratory Data Analysis & Causal Discovery**

A Streamlit web application that automates the transition from raw data to structural insights. It moves beyond standard descriptive statistics by integrating causal discovery, time series forecasting, and statistical testing directly into the exploratory phase.

## Features

### Causal Discovery
- **PC Algorithm** — Constraint-based causal DAG learning (pgmpy)
- **NOTEARS** — Gradient-based continuous optimization (causalnex)
- **GES** — Greedy Equivalence Search with BIC scoring (causal-learn)
- **LiNGAM** — Linear Non-Gaussian Acyclic Model
- **Granger Causality** — Time series causal inference
- **Double ML** — Heterogeneous treatment effect estimation

### Analysis & Forecasting
- Correlation heatmaps and scatter plots
- ACF/PACF time series analysis
- Seasonal decomposition (additive/multiplicative)
- PCA and K-means clustering
- Multi-model forecasting: SARIMAX, Prophet, VAR, MLP
- Deep learning forecasting with Temporal Convolutional Networks (TCN)
- Marketing Mix Modeling with adstock and saturation curves

### Data Support
- **Time Series** — single-entity temporal data
- **Panel Data** — multi-entity temporal data with automatic aggregation
- **Cross-Sectional** — non-temporal datasets
- Upload CSV or Parquet files, or use built-in sample datasets

## Quick Start

### Prerequisites

- Python 3.9+

### Installation

```bash
git clone https://github.com/kdan5443/Streamlit-EDA.git
cd Streamlit-EDA
pip install -r requirements.txt
```

### Run

```bash
streamlit run EDA_Streamlit.py
```

Open [http://localhost:8501](http://localhost:8501) in your browser.

### Optional Dependencies

For full functionality, install these additional libraries:

```bash
pip install causalnex causal-learn lingam prophet torch st-aggrid
```

The app works without them — features that require missing libraries are disabled gracefully.

## Application Tabs

| Tab | Description |
|-----|-------------|
| Summary | Combined PC + Granger causal analysis |
| Dashboard | Interactive 4-panel customizable dashboard |
| Correlations | Pearson heatmap and scatter plots |
| Granger | Granger causality tests and network |
| AutoDAG | Causal DAG learning (PC, NOTEARS, GES, LiNGAM) |
| Causal AI | Double ML treatment effect estimation |
| Time Series | ACF/PACF analysis |
| Panel Analysis | Per-entity time series exploration |
| Seasonality | Seasonal decomposition |
| Unsupervised | PCA and K-means clustering |
| Forecasting | SARIMAX, Prophet, VAR, MLP comparison |
| Deep Learning | Temporal Convolutional Network (TCN) |
| Marketing Mix | ROAS with adstock/saturation modeling |
| Diagnostics | ADF stationarity and Jarque-Bera normality tests |

## Tech Stack

- **UI:** Streamlit
- **Data:** Pandas, NumPy
- **Causal Discovery:** pgmpy, causalnex, causal-learn, lingam
- **Statistical Modeling:** statsmodels, scipy
- **Visualization:** Plotly, NetworkX, Matplotlib
- **ML/DL:** scikit-learn, PyTorch

## License

MIT License — see [LICENSE](LICENSE) for details.
