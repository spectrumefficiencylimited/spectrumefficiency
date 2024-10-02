# spectrumefficiency

spectrumefficiency is an R package for syncing Radio Spectrum Management (RSM) licence data from the New Zealand government API to a local DuckDB database. It provides functionality for weekly automated updates, ensuring users always have access to the latest licence information.

## Installation

You can install the development version of spectrumefficiency from GitHub with:

```r
# install.packages("devtools")
devtools::install_github("spectrumefficiency/spectrumefficiency")
```

## Usage

To set up the weekly sync:

```r
library(spectrumefficiency)
library(taskscheduleR)

# Schedule weekly sync
taskscheduleR::taskscheduler_create(
  taskname = "RSM Licence Weekly Sync",
  rscript = system.file("sync_script.R", package = "spectrumefficiency"),
  schedule = "WEEKLY",
  starttime = "23:00",
  startdate = format(Sys.Date(), "%d/%m/%Y")
)
```

To perform a manual sync:

```r
spectrumefficiency::perform_weekly_sync()
```

## Configuration

Set your RSM API key as an environment variable:

```r
Sys.setenv(RSM_API_KEY = "your_api_key_here")
```

## Functions

- `initialize_duckdb()`: Initialize the DuckDB database
- `custom_upsert_scd2()`: Perform upsert with SCD Type 2 logic
- `get_rsm_nz_data()`: Fetch data from the RSM NZ API
- `fetch_and_update_data()`: Fetch and update data in the database
- `perform_weekly_sync()`: Perform the weekly sync operation
- `perform_consistency_checks()`: Run consistency checks on the database

## Contributing

Contributions to spectrumefficiency are welcome. Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE.md file for details.
