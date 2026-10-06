# AMC Project - Innovation and Carbon Capture and Storage

## Overview

This project investigates the intersection of innovation and Carbon Capture and Storage (CCS) technologies. It leverages datasets from organizations like Stripe, Microsoft, and Frontier Climate to analyze trends and developments in the CCS domain.

## Repository Structure

```
amc_ccs/
├── amc_ccs.Rproj
├── orbis-clean-merge.R           # Orbis wide -> long, firm-year panel
├── orbis_desc_DID_R-conversion.R # R port of the Stata matching + synthetic-DiD code (from a co-author)
├── prelim_analysis.R             # Stripe / Google-patent cleaning, summary stats, preliminary regressions
├── do_files/                     # Stata: RDD motivation, patent and Orbis DiD, aggregate synthetic-DiD event studies
├── data/                         # inputs tracked in git (see below)
├── clean_outputs/                # cleaned datasets written by the scripts
├── graphs_output/                # figures
├── writeup-inprog [no github]/   # draft and presentation PDFs (July 2025)
├── z-forlatex/                   # images and a reference paper used in the write-up
└── z-dead-*.R                    # retired scripts, kept for reference, not run
```

### Data

- `data/Carbonplan_projects_20_21.csv` — 2020-21 Stripe/Microsoft applications, as compiled by CDR-CarbonPlan from Stripe's public materials (all applications, scored on six performance metrics). Project PDFs: *github.com/stripe/carbon-removal-source-materials*.
- 2022-23 Frontier Climate applications (the universe of applicants to the early-stage mechanism; winners are public, larger offtake agreements need not be, per Frontier staff). Project PDFs: *github.com/frontierclimate/carbon-removal-source-materials*. **Not in the repo** (gitignored).
- Winner/loser status: 2020-21 awards are published on Stripe's website; 2022-23 purchase agreements are on the Stripe / Frontier GitHub. Firm names were scraped from the websites, then completed by hand.
- `data/IEA_policy_data_cleaned.csv` — IEA CCUS policy data.
- `data/orbis/` — Orbis financials, downloaded spring 2024 (`historical_df_orbis.xlsx`, `orbis_gen_1.xlsx`, background docs). `orbis_long.*` / `orbis_long_2.*` are intermediate outputs, not yet tracked.
- **Gitignored, local only:** `data/stripe_data`, `data/microsoft_2022_23`, `data/PATSTAT`, `data/google_patents`.

## Key Files

| File | Role |
|---|---|
| `orbis-clean-merge.R` | Cleans the Orbis download, reshapes wide -> long and writes the dated firm-year file `orbis_long_<date>.csv` plus numeric-NA summaries |
| `prelim_analysis.R` | Cleans the Stripe data, merges manually collected Google-patent data, summary statistics and preliminary regressions on winner trends. Writes `patent_level_df.csv` and `did_df.csv` (firm x month-year, for DiD). The `summary_stats.csv` and `firm_level_data.csv` writes are currently commented out; those files in `clean_outputs/` are older copies |
| `orbis_desc_DID_R-conversion.R` | Fuzzy firm-name matching of patents to Orbis, converted from Stata (provided by a co-author); reads `orbis_long_2025-06-26.csv`, `firm_level_data.csv`, `did_df_copy.csv`; writes `250701_patent_firm_orbis.csv` |
| `do_files/*.do` | Original Stata versions (`01_RDD_motivation`, `02_patents_desc_DID`, `03_orbis_desc_DID`, `aggregate_event_SDID[_nocomp]`). Contain a hardcoded Dropbox path (`global projdir`) that must be changed |
| `z-dead-microsoft_data_cleaning.R`, `z-dead-patstat-cleaning-test.R`, `z-dead-pdf-scraping-loop.R` | Retired: Microsoft data cleaning, PATSTAT cleaning test, PDF scraping |

## Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/allegra-saggese/amc_ccs.git
   ```
2. Open `amc_ccs.Rproj` in RStudio.
3. The scripts are not chained by a runner. `orbis-clean-merge.R` and `prelim_analysis.R` are independent; `orbis_desc_DID_R-conversion.R` reads their outputs (via the `clean_outputs/` copies listed above). The gitignored raw inputs must be placed in `data/` first, and script paths should be checked (the scripts use `projdir` / relative paths).

***

##### Outputs
- Cleaned Data: Stored in clean_outputs/.
- Graphs and Visualizations: Available in graphs_output/.

##### License
No license file is currently included in the repository.

##### Contact
For questions or feedback, please contact Allegra Saggese.

## Status and planned work
Work in progress. Planned: a project-level dataset with firm characteristics, relevant CCS/CCUS policy data, and originally collected financials.
