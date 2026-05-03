# Data Dictionary

This dictionary describes the main analysis fields conceptually. Row-level values are not included in the public repository.

| Field | Description | Source category |
|---|---|---|
| `cms_id` | CMS provider identifier used as the primary hospital key after matching. | CMS |
| `cms_name` | Official CMS hospital name. | CMS |
| `google_name` | Google Places hospital/place name after matching. | Google Places API |
| `cms_county` | Hospital county used for SDOH linkage and county-clustered standard errors. | CMS / derived |
| `cms_star` | CMS overall hospital star rating. | CMS Hospital Compare |
| `clinical_score` | CMS clinical outcome domain score. | CMS Hospital Compare |
| `patient_exp_score` | CMS patient experience score. | CMS Hospital Compare |
| `google_star` | Google Maps star rating at data collection time. | Google Places API |
| `google_rating_count` | Count of Google ratings/reviews at data collection time. | Google Places API |
| `log_google_reviews` | Log-transformed Google review count. | Derived |
| `SVI_idx` | County-level Social Vulnerability Index. | AHRQ SDOH |
| `Gini_idx` | County-level Gini index. | AHRQ SDOH |
| `flag_is_kaiser` | Binary indicator for Kaiser Foundation hospitals in the California sample. Interpreted as a descriptive integrated HMO subgroup marker. | Derived |
| `flag_is_academic` | Binary indicator for academic medical centers based on CMS POS resident count and medical school affiliation fields. | CMS POS / derived |
| `google_star_pct` | Empirical percentile rank of Google star rating. | Derived |
| `cms_star_pct` | Empirical percentile rank of CMS overall star rating. | Derived |
| `clinical_score_pct` | Empirical percentile rank of CMS clinical score. | Derived |
| `patient_exp_score_pct` | Empirical percentile rank of CMS patient experience score. | Derived |
| `gap_star_pct` | Google percentile rank minus CMS overall star percentile rank. | Derived |
| `gap_google_official_exp` | Google percentile rank minus CMS patient experience percentile rank. | Derived |
| `gap_google_clinical` | Google percentile rank minus CMS clinical score percentile rank. | Derived |
