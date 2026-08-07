# Chinese Investor Sentiment and Asian Stock Markets

This repository contains the data preparation and empirical analysis for a master's dissertation on Chinese investor sentiment, Asian stock-market returns, and dynamic market correlations.

## Sample period and reproducibility

The dissertation uses a fixed sample ending on 31 August 2023. The daily DCC-GARCH dataset covers 6 January 2003 to 31 August 2023 and contains 4,296 common price observations. After log returns are calculated, the estimation sample contains 4,295 observations beginning on 7 January 2003.

The dataset is frozen so that the submitted code always uses the same sample as the dissertation. This prevents later market observations or revisions to downloaded data from changing the number of observations, estimated coefficients, tables, or figures. The analysis files therefore read local data included in this repository; re-running the analysis does not download or update the dissertation sample.

## Main analysis files

- `daily_stock_data_cleaning.ipynb` cleans and aligns the daily stock-index data and creates the frozen daily datasets.
- `Baseline_Analysis_without_SP500.ipynb` constructs the sentiment index and estimates the baseline monthly VAR and Granger-causality models without the S&P 500.
- `Extended_Analysis_with_SP500.ipynb` estimates the extended monthly analysis including the S&P 500.
- `DCC- GARCH/without S&P 500/DCC_GARCH_Asia.qmd` estimates the five-market Asian DCC-GARCH model.
- `DCC- GARCH/with S&P 500/DCC - GARCH with S&P 500.qmd` estimates the six-market DCC-GARCH model including the S&P 500.

The rendered Word documents are stored separately in the `Word output` folder inside each DCC-GARCH model folder.

## Data description

The stock-market data cover the Shanghai Composite (China), Hang Seng (Hong Kong), Nikkei 225 (Japan), KOSPI (South Korea), Singapore STI, and S&P 500 (United States). Daily data are used for the DCC-GARCH analysis, while monthly data are used for the PCA sentiment index, VAR models, and Granger-causality tests.

### Source data

- `dataset/stock/daily/` contains the six source daily stock-index price files obtained from Yahoo Finance.
- `dataset/stock/monthly/` contains the six source monthly stock-index price files obtained from Yahoo Finance.
- `dataset/Investor_Sentiment_Monthly.xlsx.xlsx` contains the monthly Chinese investor-sentiment proxies obtained from the CSMAR database and used to construct the PCA-based sentiment index (SEN).

### Prepared analysis data

- `dataset/outputs/daily_prices_all_markets.csv` contains the six markets matched by common trading date. It is the frozen price dataset used by both DCC-GARCH specifications: 4,296 observations from 6 January 2003 to 31 August 2023.
- `dataset/outputs/daily_prices_asia.csv` contains the five Asian markets matched on their own common trading dates. It is retained as a cleaning output but is not the estimation sample used to compare the two DCC-GARCH specifications.
- `dataset/outputs/stock_sentiment_dataset.xlsx` is the prepared monthly dataset for the baseline analysis without the S&P 500.
- `dataset/outputs/stock_sentiment_dataset_sp500.xlsx` is the prepared monthly dataset for the extended analysis including the S&P 500.
- `dataset/outputs/sen_and_sentiment_indicators.csv` contains SEN and its underlying sentiment indicators.

The monthly merged price-and-sentiment sample contains 248 observations from January 2003 to August 2023. The VAR samples contain 247 observations from February 2003 to August 2023 after the first observation is lost when monthly returns are calculated.

### Generated model outputs

- `daily_returns_for_dcc_no_sp500.csv` and `daily_returns_for_dcc.csv` contain the daily log returns passed to the two DCC-GARCH specifications.
- `dcc_dynamic_correlations_daily_no_sp500.csv` and `dcc_dynamic_correlations_daily.csv` contain the estimated daily dynamic conditional correlations.
- PNG files inside the two DCC-GARCH folders contain exported parameter tables and correlation figures.
- Each model's `Word output/` folder is reserved for its rendered Word and PDF documents.

The S&P 500 is not included as a variable in the baseline DCC-GARCH model, but its trading dates are used when defining the common estimation sample. This ensures that the baseline and extended models both use the same 4,295 daily return dates.

## Recommended running order

The repository already includes saved notebook outputs and frozen processed data, so the files can be inspected without re-running everything. To reproduce the workflow:

1. Run `daily_stock_data_cleaning.ipynb` to recreate the frozen daily price files.
2. Run `Baseline_Analysis_without_SP500.ipynb`.
3. Run `Extended_Analysis_with_SP500.ipynb`.
4. Render `DCC_GARCH_Asia.qmd` for the model without the S&P 500.
5. Render `DCC - GARCH with S&P 500.qmd` for the extended DCC-GARCH model.

The two DCC-GARCH specifications intentionally use the same six-market common-date sample. The baseline model excludes the S&P 500 as a model variable, but its trading dates are used to keep the two samples directly comparable.

## Python environment

Python 3.10 or later is recommended. Install the required packages from the project root with:

```bash
python -m pip install -r requirements.txt
```

The notebooks can then be opened in Jupyter Notebook, JupyterLab, or PyCharm.

## R and Quarto environment

The DCC-GARCH documents require R, Quarto, and the following R packages:

```r
install.packages(c(
  "readr", "dplyr", "lubridate", "rugarch", "rmgarch",
  "xts", "zoo", "ggplot2", "tidyr", "gt", "knitr"
))
```

Each QMD is configured to render as a Word document (`docx`). The generated document initially appears beside its QMD file and can then be moved into that model's `Word output` folder.

## Notes for assessment

- Notebook outputs are retained so that the results can be viewed directly on GitHub.
- QMD files contain the complete R analysis code.
- Rendered Word or PDF copies provide an easier-to-read version of the QMD results.
- The repository contains the source code, frozen dissertation data, and selected final outputs required to inspect the analysis.
