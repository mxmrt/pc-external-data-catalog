# Catalog Specification

## Category Modules (A-H)
- **A: Demographics and SVI** (`A_demographics_svi`)
- **B: Housing and Built Environment** (`B_housing_built_env`)
- **C: Macro, Prices, and Labor** (`C_macro_prices_labor`)
- **D: Geography and Landcover** (`D_geography_landcover`)
- **E: Climate and Environment** (`E_climate_environment`)
- **F: Weather Hazards and CAT Signals** (`F_weather_hazards_cats`)
- **G: Crime, Transport, and Utilities** (`G_crime_transport_utilities`)
- **H: Disaster, Legal, Political, and Exotic** (`H_disaster_legal_political_exotic`)

## Dataset Entry Template (Markdown)
Use this template inside each module markdown file when documenting a dataset:

```md
## Dataset: <dataset_name>
- category: <A-H module name>
- publisher: <organization>
- official_docs_url: <url or NEEDS VERIFICATION>
- data_download_url_or_api_base: <url>
- geographic_levels_available: <state/county/tract/ZIP/ZCTA/MSA/etc.>
- geo_join_keys: <exact join keys and formatting>
- temporal_resolution: <annual/monthly/daily/static>
- time_coverage_start_year: <YYYY>
- time_coverage_end_year_or_current: <YYYY/current>
- update_frequency: <annual/quarterly/monthly/ad hoc>
- example_variables: <comma-separated examples>
- access_method: <api/bulk download/file portal>
- license_or_terms_summary: <short summary>
- cost: <free/paid/mixed>
- recommended_feature_transforms: <feature engineering suggestions>
- recommended_time_alignment: <how to align to modeling year>
- expected_predictive_value: <low/medium/high + rationale>
- leakage_risk_notes: <known leakage pitfalls>
- sensitivity_proxy_flag: <NONE/POLITICAL/SENSITIVE_PROXY/POLITICAL_AND_SENSITIVE_PROXY>
- notes: <caveats, crosswalks, QA notes>
```

## Example Feature Transforms
- Per-capita rates: `metric / population * 1000` (or other scaling factor).
- Log transforms: `log1p(x)` for skewed counts/loss-like quantities.
- Rolling windows: trailing 3-year/5-year means, sums, or rates ending in year `Y-1`.
- Anomalies: difference or z-score relative to each geography's long-run baseline.
- Distances: nearest-feature distance metrics (for example coast, fault, fire station, hospital).
