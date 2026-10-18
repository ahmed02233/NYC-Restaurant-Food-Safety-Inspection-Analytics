# NYC Restaurant Food Safety — SQL Inspection Intelligence

![Restaurant Inspection Dashboard](nyc_restaurant_inspection_dashboard.png)

## Business objective
Evaluate NYC restaurant inspection violations, grades, cuisines, boroughs, and geographic/time patterns to support equitable and effective food-safety policy.

## Dataset and definitions
- Raw file: `DOHMH_New_York_City_Restaurant_Inspection_Results_20250919.csv`; raw records parsed: **13,111**.
- Proxy inspection events: **12,347**; inspection dates **1900-01-01 00:00:00** through **2025-09-16 00:00:00**.
- A source row generally represents an inspection-violation record, **not necessarily one inspection**.
- An inspection event is approximated by `CAMIS + inspection date + inspection type`; repeated same-day inspections of one type may be merged. No verified encounter identifier exists.
- Scores represent **violation points** (higher is worse), not satisfaction or performance points. Grade analysis includes A/B/C where present; unassigned/other grade events are counted separately.
- Critical status is reported status, not a causal measure. Missing values are unknown, not automatically non-critical.
- ZIP code is a geographic proxy, **not a verified neighborhood**.
- Outputs cover the actual source extract, **not necessarily all current NYC restaurants**. Avoid comparing annual totals without ensuring complete matching periods.

## Executive quality audit
| source_rows | missing_camis | missing_inspection_dates | unknown_borough_rows | missing_zip_rows | missing_street_rows | unknown_cuisine_rows | missing_grade_rows | missing_score_rows | no_violation_description_rows | missing_critical_flag_rows | earliest_inspection | latest_inspection |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 13111 | 0 | 1 | 5 | 176 | 1 | 1212 | 7400 | 1863 | 1483 | 1 | 1900-01-01 00:00:00 | 2025-09-16 00:00:00 |

## Event-key audit
| inspection_events | source_rows_in_events | conflicting_grades | conflicting_scores | conflicting_boroughs | conflicting_cuisines | multi_row_inspections |
| --- | --- | --- | --- | --- | --- | --- |
| 12347 | 13110.0 | 0.0 | 0.0 | 0.0 | 0.0 | 717.0 |

## Annual inspection trend
| year | inspection_events | graded_events | avg_violation_score | pct_a_among_abc |
| --- | --- | --- | --- | --- |
| 1900 | 1211 | 0 | — | — |
| 2016 | 9 | 6 | 9.75 | 100.0 |
| 2017 | 13 | 10 | 17.77 | 70.0 |
| 2018 | 35 | 16 | 22.34 | 81.25 |
| 2019 | 33 | 15 | 25.21 | 66.67 |
| 2020 | 19 | 8 | 23.13 | 75.0 |
| 2021 | 194 | 74 | 19.39 | 90.54 |
| 2022 | 2110 | 912 | 20.86 | 78.07 |
| 2023 | 2630 | 1240 | 23.63 | 74.6 |
| 2024 | 3525 | 1589 | 25.0 | 73.63 |
| 2025 | 2568 | 984 | 25.97 | 78.96 |

## Inspections and grades by borough
| borough | inspection_events | graded_events | pct_a_among_abc | avg_violation_score | pct_events_with_critical |
| --- | --- | --- | --- | --- | --- |
| MANHATTAN | 4587 | 1818 | 78.66 | 22.85 | 50.38 |
| BROOKLYN | 3246 | 1244 | 75.16 | 24.56 | 52.71 |
| QUEENS | 2988 | 1159 | 73.08 | 25.71 | 54.38 |
| BRONX | 1091 | 450 | 75.33 | 22.91 | 53.8 |
| STATEN ISLAND | 431 | 183 | 77.6 | 21.4 | 54.76 |
| UNKNOWN | 4 | 0 | — | — | 0.0 |

## NYC grade distribution
| grade_group | inspection_events |
| --- | --- |
| UNASSIGNED/OTHER | 7493 |
| A | 3693 |
| B | 697 |
| C | 464 |

## Most frequent inspection types
| inspection_type | inspection_events |
| --- | --- |
| CYCLE INSPECTION / INITIAL INSPECTION | 5831 |
| CYCLE INSPECTION / RE-INSPECTION | 2295 |
| PRE-PERMIT (OPERATIONAL) / INITIAL INSPECTION | 1414 |
| UNKNOWN | 1211 |
| ADMINISTRATIVE MISCELLANEOUS / INITIAL INSPECTION | 451 |
| PRE-PERMIT (OPERATIONAL) / RE-INSPECTION | 419 |
| CYCLE INSPECTION / REOPENING INSPECTION | 157 |
| PRE-PERMIT (NON-OPERATIONAL) / INITIAL INSPECTION | 122 |
| INTER-AGENCY TASK FORCE / INITIAL INSPECTION | 94 |
| ADMINISTRATIVE MISCELLANEOUS / RE-INSPECTION | 84 |

## Top 10 violation mentions
| violation_code | violation_description | mentions | critical_mentions |
| --- | --- | --- | --- |
| 10F | Non-food contact surface or equipment made of unacceptable material, not kept clean, or not properly sealed, raised, spaced or movable to allow accessibility for cleaning on all sides, above and underneath the unit. | 1066 | 0 |
| 08A | Establishment is not free of harborage or conditions conducive to rodents, insects or other pests. | 1064 | 0 |
| 02B | Hot TCS food item not held at or above 140 °F. | 1011 | 1011 |
| 04L | Evidence of mice or live mice in establishment's food or non-food areas. | 819 | 819 |
| 06D | Food contact surface not properly washed, rinsed and sanitized after each use and following any activity when contamination may have occurred. | 740 | 740 |
| 02G | Cold TCS food item held above 41 °F; smoked or processed fish held above 38 °F; intact raw eggs held above 45 °F; or reduced oxygen packaged (ROP) TCS foods held above required temperatures except during active necessary preparation. | 449 | 449 |
| 10B | Anti-siphonage or back-flow prevention device not provided where required; equipment or floor not properly drained; sewage disposal system in disrepair or not functioning properly. Condensation or liquid waste improperly disposed of. | 425 | 0 |
| 04A | Food Protection Certificate (FPC) not held by manager or supervisor of food operations. | 364 | 364 |
| 04M | Live roaches in facility's food or non-food area. | 348 | 348 |
| 06C | Food, supplies, or equipment not protected from potential source of contamination during storage, preparation, transportation, display, service or from customer’s refillable, reusable container. Condiments not in single-service containers or dispensed directly by the vendor. | 336 | 336 |

A single event may contain multiple different violation mentions. Mentions are not unique restaurants or inspections.

## Critical vs non-critical violation rows
| critical_status | violation_rows |
| --- | --- |
| CRITICAL | 6739 |
| NOT CRITICAL | 4809 |
| OTHER/UNKNOWN | 80 |

## Highest-scoring cuisines (worse reported violation points)
Uses at least 30 proxy inspection events per cuisine; exploratory only, not an exposure-adjusted restaurant risk estimate.
| cuisine | inspection_events | avg_violation_score | pct_a_among_abc | pct_events_with_critical |
| --- | --- | --- | --- | --- |
| BANGLADESHI | 52 | 41.53 | 61.11 | 71.15 |
| AFRICAN | 49 | 32.94 | 52.63 | 61.22 |
| TURKISH | 34 | 30.71 | 63.64 | 50.0 |
| JEWISH/KOSHER | 141 | 29.96 | 53.7 | 56.74 |
| INDIAN | 163 | 29.17 | 60.71 | 65.03 |

## ZIP / geographic analysis
`nyc_inspection_zip_summary.csv` includes ZIP-level proxy event counts and rates. Borough counts are not per-restaurant risk rates; repeated inspections are common, and restaurant mix varies.

## Methodology and validation
1. Scan large CSV using DuckDB SQL with nullable, tolerant parsing; irrecoverably malformed rows may be skipped and must be separately reconciled for official reporting.
2. Inspect fields against the supplied data dictionary and audit missing dates, boroughs, ZIP codes, cuisines, and grades.
3. Standardize commonly equivalent cuisine labels conservatively and convert inspection/grade dates.
4. Construct proxy inspection-level events to avoid counting violation rows as separate inspections.
5. Audit conflicting grades, scores, boroughs and cuisines within inspection events. Conflicting A/B/C grades are unassigned rather than arbitrarily selected.
6. Generate SQL summaries; reconcile event totals between annual, borough and grade exports.
7. Save charts, CSV outputs, recommendations and a ZIP package.

## Business recommendations
See [RECOMMENDATIONS.md](RECOMMENDATIONS.md) for seven prioritized, measurable recommendations. Largest raw volume is not the same as greatest safety risk.

## Technology
Python, DuckDB SQL, pandas, NumPy, Matplotlib and Google Colab. This release includes a static Python dashboard and Power BI-ready CSVs; **no finished Power BI report**.

## Reproduction
1. Obtain the NYC DOHMH restaurant inspection CSV from the original assignment or authorized NYC open-data source, verify the data dictionary and licensing.
2. Upload `NYC_Restaurant_Inspection_SQL_Analysis.ipynb` to Google Colab.
3. Upload the source CSV to `/content` or Google Drive; set `DATA_FILE` in Cell 1 if needed.
4. Run cells 1–7 and check printed `VALIDATION: PASS` and `PACKAGE READY` messages.
5. Read exports from `/content/NYC_Project8_Outputs`. Download the notebook `.ipynb` separately and add it to the extracted ZIP files before GitHub publishing.

## Limitations
Data feed may contain updated, administrative, and ungraded records; the proxy event key may merge inspections. Missing grades are not failures. Cuisine normalization is limited; score differences may reflect inspection type and selection effects. Annual trends may have incomplete boundary-year coverage. ZIP codes are not neighborhoods. Rates by borough or cuisine are conditioned on recorded inspections, not all restaurants. No official individual-restaurant or neighborhood risk ranking is claimed. The original raw CSV is excluded from the ZIP by default because of its possible large size.

## GitHub publishing
**Repository:** `NYC-Restaurant-Food-Safety-Inspection-Analytics`  
**Description:** SQL-based NYC restaurant inspection analytics exploring food safety violations, grades, cuisine patterns, geographic differences, and targeted policy actions.  
**Create repository:** https://github.com/new
