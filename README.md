# Divergence Between Google Maps Reviews and CMS Hospital Ratings in California

|                  |                                                                           |
| ---------------- | ------------------------------------------------------------------------- |
| **Domain**       | Healthcare analytics, public ratings                                      |
| **Sample**       | 239 California hospitals, 42 counties                                     |
| **Methods**      | Fuzzy entity matching, county-clustered OLS, nonparametric tests          |
| **Stack**        | Python · pandas · RapidFuzz · statsmodels · scikit-learn · folium         |
| **Data sources** | Google Places API · CMS Hospital Compare · AHRQ SDOH · CMS POS File       |
| **My Role**      | Entity resolution, preprocessing, statistical modeling, technical writing |

Google hospital ratings are widely used but rarely validated against clinical quality measures. This project examines whether Google Maps hospital ratings align with official CMS hospital quality measures among 239 California hospitals across 42 counties.

## Key Findings

- **Google ratings are not a reliable proxy for clinical quality.**  
  Google star ratings show weak alignment with CMS clinical quality scores, even though they are somewhat more aligned with CMS patient experience. This suggests that online ratings should not be used alone for clinical-quality interpretation.

- **Review volume behaves like a platform visibility signal.**  
  Hospitals with more Google reviews tend to rank higher on Google relative to CMS measures, while review count is not meaningfully associated with CMS overall stars. For analytics teams, this means review volume should be treated as a potential platform-exposure factor, not just a popularity metric.

- **Institutional subgroup patterns matter.**  
  Kaiser / integrated HMO hospitals and academic medical centers show different Google–CMS divergence patterns. This suggests that hospital type should be accounted for when comparing public-facing reputation with official quality metrics.

- **County-level vulnerability affects both systems, but does not explain the gap.**  
  Social vulnerability is negatively associated with both Google and CMS ratings, but it does not significantly widen the Google–CMS percentile gap. In this dataset, divergence is more closely associated with review volume and institutional subgroup patterns than with county-level SDOH alone.

Overall, online ratings appear to capture public-facing experience and visibility more than clinical quality.

## Selected Outputs

### Rating Distributions

![Rating distributions](outputs/figures/01_rating_distributions.png)

Four rating variables plotted separately. Scales and distributions differ across systems, motivating percentile-rank gap outcomes rather than raw-score comparison.

### Spearman Correlation Heatmap

![Spearman correlation heatmap](outputs/figures/02_spearman_correlation_heatmap.png)

Spearman rank correlations between Google and CMS measures. Google star ratings show weak alignment with CMS clinical quality scores (ρ = 0.09).

### Google vs. CMS Clinical Percentile Gap Bubble Plot

![Google vs. CMS clinical rank bubble](outputs/figures/04_google_cms_clinical_rank_bubble.png)

Each point is one hospital. Points above the diagonal rank higher on Google than on CMS clinical quality. Bubble size reflects Google review count; color indicates institutional subgroup.

### Coefficient Forest Plot

![Coefficient Forest Plot](outputs/figures/08_institutional_subgroup_coefficients.png)

Coefficient estimates (95% CI) for Kaiser and Academic Medical Center indicators across five models. Both institutional types receive higher CMS overall stars, but diverge in gap-model direction.

### Redacted Interactive Map Preview

![Redacted Folium map preview](outputs/maps/folium_interactive_popup_redacted_preview.png)

Interactive Folium map of hospital locations across California. Popup fields are redacted in this preview.

## Repository Structure

```text
.
├── README.md
├── notebooks/
│   ├── 02_fuzzy_matching.ipynb
│   ├── 04_dataset_merge.ipynb
│   ├── 05_preprocessing_eda.ipynb
│   ├── 06_ols_modeling_sensitivity.ipynb
│   └── 07_interactive_map.ipynb
├── outputs/
│   ├── figures/
│   ├── tables/
│   └── maps/
├── data/
│   ├── README.md
│   └── data_dictionary.md
└── docs/
    └── methodology_notes.md
```

## Notebook Guide

| Notebook | Purpose |
|---|---|
| `02_fuzzy_matching.ipynb` | ZIP3-constrained fuzzy matching between CMS hospital names and Google place names, with geographic validation and manual review logic. |
| `04_dataset_merge.ipynb` | Final merge across Google-derived records, CMS quality files, AHRQ county SDOH indicators, and CMS POS teaching variables. |
| `05_preprocessing_eda.ipynb` | Exclusions, missing-data handling, Kaiser and academic flags, percentile ranks, nonparametric tests, and aggregate EDA figures. |
| `06_ols_modeling_sensitivity.ipynb` | County-clustered OLS models, coefficient plots, diagnostics, Kaiser exclusion sensitivity, and Cook's-distance sensitivity. |
| `07_interactive_map.ipynb` | Folium-based interactive map workflow. |

## My Contributions

This project was completed by a three-person team for UC Davis STA 220. This public version focuses on the analytical workflow I owned end-to-end: 

- **Entity resolution:** Built a proof-of-concept Google Places API querying demo and the ZIP3-constrained fuzzy matching pipeline (RapidFuzz) linking 250 CMS hospital records to Google Places entries, including geographic validation; diagnosed incomplete Southern California coverage as an API pagination limit and designed a targeted re-query.
- **Statistical modeling**: Specified and estimated five county-clustered OLS models; conducted Spearman/Wilcoxon tests and two sensitivity analyses (Kaiser exclusion, Cook's distance).
- **Preprocessing**: Handled Kaiser clinical-score missingness as an MNAR institutional pattern; constructed AMC indicator; constructed percentile-rank gap outcomes.
- **Technical writing:** Rewrote the methodology, results, and discussion sections to correct statistical interpretation issues and align the final report with the actual analysis.

## Limitations

- California-only sample; institutional patterns may not generalize to other states.
- Cross-sectional design; Google ratings and CMS measures do not necessarily reflect identical time windows.
- Google reviewers are self-selected and may not represent the full patient population.
- Subgroup estimates for academic medical centers and the Kaiser / integrated HMO marker should be interpreted cautiously because subgroup sizes are limited.
- All associations are descriptive.

## Repository Scope

This is a portfolio case study, not an end-to-end reproducibility package. Raw Google API outputs, row-level merged data, and teammate-authored notebooks are not included. See `data/README.md` for data source details. Notebooks are provided for workflow review; outputs are cleared because source data are excluded.

## Tools

Python, pandas, NumPy, RapidFuzz, statsmodels, scipy, scikit-learn, matplotlib, seaborn, folium.
