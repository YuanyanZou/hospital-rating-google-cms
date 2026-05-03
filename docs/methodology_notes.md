# Methodology Notes

These notes summarize the public-facing analysis workflow. Result wording follows the official LaTeX report; contribution boundaries follow the project experience document.

## Entity Resolution

CMS and Google use different naming conventions for the same hospitals, so exact name matching was insufficient. The matching workflow used:

- ZIP3-constrained candidate generation to reduce false positives.
- RapidFuzz `token_set_ratio` scoring within local candidate pools.
- Top-candidate review using a similarity threshold.
- ZIP5 geographic validation to separate high-confidence matches from cases needing review.
- Diagnosis of a Southern California unmatched cluster as an upstream API completeness issue rather than a fuzzy matching failure.

The matching diagnosis was a central part of the project: the unresolved cases were geographically concentrated, which pointed to incomplete first-pass Google retrieval rather than only poor string similarity.

This step is included as workflow documentation; raw Google API-derived records are excluded from the public repo.

## Preprocessing

The final analytic sample contained 239 California hospitals after excluding hospitals without CMS overall star ratings and one specialty facility that was not comparable within the matched design.

Key feature decisions:

- Google review count was log-transformed because the original distribution was strongly right-skewed.
- Google review count, SVI, and Gini were standardized to z-scores for comparability across models.
- Google and CMS measures were converted to empirical percentile ranks for gap outcomes because the original rating systems use different scales and distributions; the gap is interpreted as a relative standing difference, not a raw score difference.

**Kaiser / integrated HMO hospitals**  
23 of 30 Kaiser hospitals had structurally missing CMS clinical scores. This missingness was treated as MNAR rather than random: Kaiser's integrated HMO model means most facilities do not meet CMS reporting thresholds by design, not because data was unavailable. Listwise deletion would have removed 12.6% of the sample and systematically excluded this institutional type. All 30 Kaiser hospitals were retained with a binary indicator flag.

**Academic Medical Center indicator**  
The AMC indicator emerged mid-analysis: Kaiser's gap pattern prompted a closer look at other institutionally distinct hospital types, and UC system hospitals had been noticeably difficult to resolve during fuzzy matching — suggesting a structurally different naming and reporting pattern. AMCs were defined using dual criteria from the CMS Provider of Services file: resident physician count > 200 and medical school affiliation code = 1, validated against Definitive Healthcare's California AMC reference list (n=15 matched exactly).

## Models

The analysis estimated two baseline models and three percentile-gap models:

- Baseline Google star rating.
- Baseline CMS overall star rating.
- Google minus CMS overall star percentile gap.
- Google minus CMS patient experience percentile gap.
- Google minus CMS clinical outcome percentile gap.

All models used OLS with county-clustered robust standard errors. Clustering was used because hospitals within a county may share unobserved healthcare-market and policy conditions, and because SVI and Gini are county-level covariates assigned to hospitals within the same county.

## Result Interpretation

All model results are interpreted descriptively.

The official report found that Google ratings were only weakly associated with CMS clinical scores and modestly associated with CMS patient experience scores. Standardized log review count was the most stable positive correlate across Google-facing outcomes and percentile-gap outcomes, while it was not statistically associated with CMS overall stars. Social vulnerability was negatively associated with both Google and CMS ratings but was not significantly associated with the gap outcomes.

Institutional subgroup coefficients are reported as descriptive associations. The analysis does not claim that HMO integration, academic status, review volume, or county socioeconomic conditions causally change ratings.

## Sensitivity Checks

Two sensitivity checks were included:

- Excluding Kaiser hospitals.
- Removing influential observations using Cook's distance.

The official report states that review-count associations and academic medical center gap patterns remained qualitatively consistent under these checks.
