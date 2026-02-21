# P&C External Dataset Catalog Instructions

## Purpose
This repository maintains a catalog of external datasets that can be merged onto P&C modeling tables using both geo join keys and time join keys.

## Output Files Spec
Use the following standardized files under `research/`:

- `research/CATALOG_SPEC.md`
- `research/A_demographics_svi.md`
- `research/A_demographics_svi.csv`
- `research/B_housing_built_env.md`
- `research/B_housing_built_env.csv`
- `research/C_macro_prices_labor.md`
- `research/C_macro_prices_labor.csv`
- `research/D_geography_landcover.md`
- `research/D_geography_landcover.csv`
- `research/E_climate_environment.md`
- `research/E_climate_environment.csv`
- `research/F_weather_hazards_cats.md`
- `research/F_weather_hazards_cats.csv`
- `research/G_crime_transport_utilities.md`
- `research/G_crime_transport_utilities.csv`
- `research/H_disaster_legal_political_exotic.md`
- `research/H_disaster_legal_political_exotic.csv`

## CSV Schema (Exact Column Order)
All catalog CSV files must use this exact header row and column order:

`category,dataset_name,publisher,geographic_levels_available,geo_join_keys,temporal_resolution,time_coverage_start_year,time_coverage_end_year_or_current,update_frequency,example_variables,access_method,official_docs_url,data_download_url_or_api_base,license_or_terms_summary,cost,recommended_feature_transforms,recommended_time_alignment,expected_predictive_value,leakage_risk_notes,sensitivity_proxy_flag,notes`

## Time Alignment and Leakage Rules
- Default temporal join: for modeling year `Y`, join external context from year `Y-1`.
- Event data: compute trailing windows that end in `Y-1` (not in `Y`).
- Static-by-geo data: replicate value across years for each geo key and mark as static.
- Any exception to prior-year alignment must be explicitly justified and flagged in `leakage_risk_notes`.

## Geo Key Conventions
- Store FIPS codes as zero-padded strings.
- State FIPS: 2-digit string (for example `01`).
- County FIPS: 5-digit string including state prefix (for example `01001`).
- Census tract GEOID: 11-digit string, no decimals, keep leading zeros.
- ZIP and ZCTA are not interchangeable: document which one a dataset uses and required crosswalk logic.
- For lat/lon sources, roll up to target geographies via deterministic spatial join and record boundary vintage/source.

## Quality Bar
- Every dataset entry must include an official documentation URL in `official_docs_url`.
- If internet access is unavailable, set verification status clearly by writing `NEEDS VERIFICATION` and document why in `notes`.

## Sensitivity Flag Rule
- Political variables and sensitive/proxy variables must be explicitly labeled in `sensitivity_proxy_flag`.
- Use clear labels such as `NONE`, `POLITICAL`, `SENSITIVE_PROXY`, or `POLITICAL_AND_SENSITIVE_PROXY`.
