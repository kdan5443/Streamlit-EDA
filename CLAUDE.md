# CLAUDE.md

## Project Overview

Streamlit-EDA is an interactive Streamlit web application for causal discovery and exploratory data analysis. It automates the transition from raw data to structural insights by integrating causal discovery, correlation analysis, time series forecasting, and statistical testing.

## Repository Structure

```
Streamlit-EDA/
├── EDA_Streamlit.py           # Main application code (~1776 lines)
├── requirements.txt           # Python dependencies
├── .streamlit/config.toml     # Streamlit theme and server config
├── .gitignore
├── LICENSE                    # MIT License
├── README.md                  # Project documentation
└── CLAUDE.md                  # This file
```

All application logic lives in a single file: `EDA_Streamlit.py`.

## Running the Application

```bash
pip install -r requirements.txt
streamlit run EDA_Streamlit.py
```

The app runs at `http://localhost:8501` by default. Streamlit auto-reloads on file save.

## Dependencies

**Core (required):** streamlit, pandas, numpy, pgmpy, statsmodels, scipy, plotly, networkx, matplotlib, scikit-learn

**Optional (imported via try/except):** causalnex, causal-learn, lingam, prophet, torch, st_aggrid. Missing optional libraries degrade gracefully.

## Code Architecture

### File Layout (EDA_Streamlit.py)

| Section | Lines | Description |
|---------|-------|-------------|
| Imports | 1–82 | All library imports, optional ones wrapped in try/except |
| Config/CSS | 83–115 | `GLOBAL_SEED=42`, page config, dark-mode CSS |
| Sidebar | 116–143 | File upload, datetime/entity column selection, sample data |
| Helper functions | 145–730 | All computation and visualization logic |
| Session state | 785–805 | `st.session_state.results` initialization |
| Main UI (14 tabs) | 840–1776 | Tab-based analysis interface |

### Function Naming Conventions

- `_prefix` — internal helpers (`_load_data`, `_coerce_numeric`, `_validate_time_index`)
- `fig_` — figure/chart generators (`fig_timeseries`, `fig_corr_heatmap`, `fig_cpdag_plotly`)
- `compute_` — data computations (`compute_corr`, `compute_adf_stationary`)
- `run_` — analysis orchestrators (`run_granger_causality_summary`)
- `classify_` — DAG node classifiers (`classify_nodes`, `classify_granger_nodes`)

### The 14 Analysis Tabs

0. **Summary** — Combined PC + Granger causal analysis
1. **Dashboard** — Interactive 4-panel customizable dashboard
2. **Correlations** — Pearson heatmap and scatter plots
3. **Granger** — Granger causality tests and network
4. **AutoDAG** — Causal DAG learning (PC, NOTEARS, GES, LiNGAM)
5. **Causal AI** — Double ML for treatment effect estimation
6. **Time Series** — ACF/PACF analysis
7. **Panel Analysis** — Per-entity time series exploration
8. **Seasonality** — Seasonal decomposition
9. **Unsupervised** — PCA and K-means clustering
10. **Forecasting** — SARIMAX, Prophet, VAR, MLP comparison
11. **Deep Learning** — Temporal Convolutional Network (TCN)
12. **Marketing Mix** — ROAS with adstock/saturation modeling
13. **Diagnostics** — ADF stationarity and Jarque-Bera normality tests

## Key Patterns

### Caching

All expensive computations use `@st.cache_data(show_spinner=...)` to avoid recomputation on UI interaction.

### Data Type Detection

The app auto-detects three data types based on the index:
- **Time Series** — valid datetime index, no duplicates
- **Panel Data** — valid datetime index with duplicates (multiple entities)
- **Cross-Sectional** — no datetime index

Panel data is aggregated by daily mean when algorithms require a unique time index.

### Color Scheme (Dark Theme)

Configured in `.streamlit/config.toml` and reinforced with inline CSS.

- `#16a34a` (green) — Root/Driver nodes
- `#dc2626` (red) — Effect/Outcome nodes
- `#00c2ff` (cyan) — Mediator nodes
- `#ff7a00` (orange) — Ambiguous/undirected edges
- Background: `#0b0f17`, Text: `#e5e7eb`

### Error Handling

- Optional library imports fail silently with fallback
- User-facing errors via `st.error()` / `st.warning()`
- Data validation before each analysis step

### Session State

Results are stored in `st.session_state.results` (dict), persisted across tabs within a session. Download buttons export CSV, PNG, GraphML, or JSON.

## Development Guidelines

- Keep all code in the single `EDA_Streamlit.py` file (monolithic architecture)
- Use `@st.cache_data` for any new computation functions
- Follow existing naming conventions (`fig_`, `compute_`, `_private`)
- Wrap optional dependency imports in try/except blocks
- Use Plotly for interactive charts; maintain the dark color scheme
- Test with both uploaded CSV/Parquet files and built-in sample datasets ("Synthetic Trending", "Seasonal + Noise")
- Global random seed is `GLOBAL_SEED = 42`
