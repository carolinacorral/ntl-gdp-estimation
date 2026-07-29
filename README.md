# ntl-gdp-estimation

Code and notebooks for estimating Mexican municipality-level GDP using VIIRS nighttime lights (NTL).

This repository accompanies the chapter:

**García, Claudia; Corral, Carolina; and Lopez, Jesús Manuel.**  
*Predictive Model to Estimate the Economic Activity of Mexican Municipalities Using Night Lights*  
In *Quantitative Finance Programming: Models, Methods, and Business Applications* (IGI Global, 2027).  
DOI: [`10.4018/979-8-3373-8372-9.ch011`](https://doi.org/10.4018/979-8-3373-8372-9.ch011)

## Overview

The project evaluates whether nighttime-light intensity can be used as a proxy for local economic activity in Mexico, where GDP is typically available at higher geographic levels but not as a regular municipal series.

The repository contains preprocessing notebooks, exploratory analysis, and model experiments using:

- OLS
- Random Forest
- hybrid OLS + Random Forest approaches

## Repository Structure

```text
.
├── notebooks/
│   ├── preprocessing/
│   │   ├── 01_oaxaca.ipynb
│   │   └── 02_cdmx.ipynb
│   ├── eda/
│   │   ├── 01_linealidad.ipynb
│   │   └── del.md
│   └── experiments/
│       ├── 01_models_oaxaca.ipynb
│       ├── 02_ols_no_lags_cdmx.ipynb
│       └── 03_elasticity.ipynb
├── data/
│   ├── raw-data/
│   │   ├── 01_raw_ntl_data.csv.zip
│   │   ├── 02_raw_gdp_data_cdmx.csv
│   │   └── del.md
│   ├── cdmx_pib_municipio.csv
│   ├── pib_trimestral_izt.csv
│   ├── serie_pib_trimestral_cdmx.csv
│   ├── serie_rad_pib_cdmx_desestacionalizada.csv
│   ├── serie_trimestral_cdmx_desestacionalizada(sin agg).csv
│   ├── serie_trimestral_cdmx_desestacionalizada_agg.csv
│   ├── serie_trimestral_oax_desestacionalizada_agg.csv
│   └── data.md
├── code/
│   └── NTL/
│       └── NTL_Iztapala.ipynb
├── NTL_Iztapala_GDp.ipynb
└── README.md
```

## Setup

```bash
git clone https://github.com/carolinacorral/ntl-gdp-estimation.git
cd ntl-gdp-estimation

python -m venv .venv
source .venv/bin/activate

pip install --upgrade pip
pip install pandas numpy scipy matplotlib seaborn scikit-learn statsmodels gdown jupyterlab
```

Run notebooks with:

```bash
jupyter lab
```

## Reproducing the Results

Suggested order:

1. `notebooks/preprocessing/01_oaxaca.ipynb`  
   Builds the Oaxaca quarterly municipality-level dataset.

2. `notebooks/preprocessing/02_cdmx.ipynb`  
   Builds the CDMX datasets, including deseasonalized and aggregated NTL-GDP files.

3. `notebooks/eda/01_linealidad.ipynb`  
   Explores the linearity of the NTL-GDP relationship and model diagnostics.

4. `notebooks/experiments/01_models_oaxaca.ipynb`  
   Runs Oaxaca model comparisons across OLS, Random Forest, and hybrid specifications.

5. `notebooks/experiments/02_ols_no_lags_cdmx.ipynb`  
   Runs the main CDMX experiment.

6. `notebooks/experiments/03_elasticity.ipynb`  
   Computes elasticity-style summaries and additional time-series checks.

Legacy / prototype notebooks:

- `NTL_Iztapala_GDp.ipynb`
- `code/NTL/NTL_Iztapala.ipynb`

These focus on Iztapalapa and are useful as earlier municipality-specific analyses, but they are separate from the numbered workflow above.

## Data Sources

### Nighttime lights

The project uses **VIIRS Day/Night Band nighttime lights**. The repository includes a raw municipality-date level extract in:

- `data/raw-data/01_raw_ntl_data.csv.zip`

Official source:

- [Earth Observation Group (EOG) VIIRS Nighttime Light Data](https://eogdata.mines.edu/products/vnl/)

### GDP data

The project uses GDP inputs derived from official Mexican statistical sources. The repository includes intermediate GDP-based files such as:

- `data/raw-data/02_raw_gdp_data_cdmx.csv`
- `data/cdmx_pib_municipio.csv`
- `data/serie_pib_trimestral_cdmx.csv`

Official starting points:

- [INEGI Banco de Información Económica](https://www.inegi.org.mx/sistemas/bie/)
- [INEGI Producto Interno Bruto por Entidad Federativa](https://www.inegi.org.mx/programas/pibent/)
- [INEGI Censo de Población y Vivienda 2020](https://www.inegi.org.mx/programas/ccpv/2020/default.html)

Municipal GDP is not available as a regular official time series in Mexico, so the municipal series used here are constructed from higher-level GDP data and municipal allocation rules described in the chapter.

## Notes

Some notebooks still contain `gdown` cells with placeholder values such as `url = 'drive url'`. In practice, you can either:

- use the files already committed under `data/`, or
- replace the placeholder URLs with your own stored copies of the intermediate CSVs

## Citation

If you use this repository, please cite the associated chapter.

### Suggested citation

```text
Corral, C., García, C., & Lopez, J. M. (2027).
Predictive Model to Estimate the Economic Activity of Mexican Municipalities Using Night Lights.
In Quantitative Finance Programming: Models, Methods, and Business Applications.
IGI Global. https://doi.org/10.4018/979-8-3373-8372-9.ch011
```

### BibTeX

```bibtex
@incollection{corral2027_ntl_gdp_mexico,
  author    = {Corral, Carolina and García, Claudia and Lopez, Jesús Manuel},
  title     = {Predictive Model to Estimate the Economic Activity of Mexican Municipalities Using Night Lights},
  booktitle = {Quantitative Finance Programming: Models, Methods, and Business Applications},
  publisher = {IGI Global},
  year      = {2027},
  doi       = {10.4018/979-8-3373-8372-9.ch011}
}
```
