# Chinese Investor Sentiment and Asian Stock Markets

This repository contains the data preparation and empirical analysis for a master's dissertation on Chinese investor sentiment, Asian stock-market returns, and dynamic market correlations.

## Sample and frozen data

The dissertation uses a fixed sample ending on 31 August 2023. The daily DCC-GARCH dataset covers 6 January 2003 to 31 August 2023 and contains 4,296 common price observations. After log returns are calculated, the estimation sample contains 4,295 observations beginning on 7 January 2003.

The analysis files read local data included in this repository. Re-running the analysis does not download or update the frozen dissertation sample.

## Main analysis files

- `daily_stock_data_cleaning.ipynb` cleans and aligns the daily stock-index data and creates the frozen daily datasets.
- `Baseline_Analysis_without_SP500.ipynb` constructs the sentiment index and estimates the baseline monthly VAR and Granger-causality models without the S&P 500.
- `Extended_Analysis_with_SP500.ipynb` estimates the extended monthly analysis including the S&P 500.
- `DCC- GARCH/without S&P 500/DCC_GARCH_Asia.qmd` estimates the five-market Asian DCC-GARCH model.
- `DCC- GARCH/with S&P 500/DCC - GARCH with S&P 500.qmd` estimates the six-market DCC-GARCH model including the S&P 500.

The rendered Word documents are stored separately in the `Word output` folder inside each DCC-GARCH model folder.

## Data folders

- `dataset/stock/daily/` contains the source daily stock-index files.
- `dataset/stock/monthly/` contains the source monthly stock-index files.
- `dataset/outputs/daily_prices_all_markets.csv` is the frozen common-date dataset used by both DCC-GARCH specifications.
- `dataset/outputs/daily_prices_asia.csv` contains the five Asian markets over their common trading dates.
- `dataset/outputs/stock_sentiment_dataset.xlsx` and `stock_sentiment_dataset_sp500.xlsx` are the prepared monthly datasets.
- `archive/` contains old data copies extending beyond the dissertation sample and is not used by the analysis.

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
- Files inside `archive/`, temporary Word files beginning with `~$`, Quarto `*_files/` folders, and `.rmarkdown` intermediates are not part of the submitted analysis.
