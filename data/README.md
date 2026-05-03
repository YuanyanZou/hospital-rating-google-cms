# Data Availability

This public portfolio repository does not include row-level data.

The original project used:

- **Google Places API:** hospital names, star ratings, review counts, addresses, and geographic coordinates.
- **CMS Hospital Compare:** hospital overall star ratings, clinical outcome scores, and patient experience scores.
- **AHRQ SDOH Database:** county-level Social Vulnerability Index and Gini index.
- **CMS Provider of Services File:** resident physician counts and medical school affiliation fields used to construct the academic medical center indicator.

## Why Data Are Excluded

Raw Google API outputs and merged row-level analytic files are excluded because they contain API-derived fields and project-specific intermediate records. Some upstream collection code was also teammate-authored and is not included in this individual portfolio reconstruction.

The notebooks are therefore provided for code review and methodological transparency. They are not presented as a fully runnable public reproduction package.

## Expected Local Inputs

The sanitized notebooks reference local filenames from the original project workflow, including Google-derived, CMS, AHRQ, and intermediate merge files. To rerun the notebooks, a user would need to obtain source data independently and reconstruct the expected local inputs.

## Public Outputs

This repository includes aggregate figures, aggregate markdown tables, and one tiny statewide map overview. These public outputs are intended to communicate the analysis without exposing row-level records.
