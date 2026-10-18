# NYC Restaurant Inspection — Policy Recommendations

## Decision standard
Findings are descriptive associations in recorded inspections, not proof of restaurant, neighborhood or cuisine-specific inherent risk. Validate individual enforcement decisions using current records, case history, and consistent policies.

## 1. Prioritize repeat critical violations (Critical)
**Evidence:** Critical-violation-bearing inspection events are measured by borough and cuisine.
**Action:** Identify repeat patterns at the restaurant level after reconciling events; schedule fair, risk-based follow-ups.
**Measure:** Verified repeat critical violations per inspected restaurant and follow-up compliance.

## 2. Target the most frequent specific violations (High)
**Evidence:** Most frequently mentioned description: **Non-food contact surface or equipment made of unacceptable material, not kept clean, or not properly sealed, raised, spaced or movable to allow accessibility for cleaning on all sides, above and underneath the unit.**.
**Action:** Provide issue-specific operator training and publish clear inspection checklists.
**Measure:** Subsequent violation mentions per reinspection, controlling for inspection type.

## 3. Validate low-performance cuisine segments before intervention (High)
**Evidence:** Highest average violation points among cuisines with >=30 proxy events: **BANGLADESHI**.
**Action:** Examine sample size, inspection mix and repeated establishments before tailoring language-accessible education.
**Measure:** Score improvement among comparable inspection types and cohorts; no stereotype-based enforcement.

## 4. Investigate geographic concentrations (High)
**Evidence:** Borough and ZIP code reports show counts and critical-event shares.
**Action:** Validate hotspots using street address, inspection history and number of active inspected restaurants; prioritize on-site technical assistance.
**Measure:** Critical events per completed inspection by comparable period and inspection type.

## 5. Improve grade transparency (High)
**Evidence:** Ungraded and other records are separated from A/B/C grade counts.
**Action:** Track grade assignment status by inspection type and time; ensure clear public definitions.
**Measure:** Share of eligible graded inspections with documented grades.

## 6. Harmonize restaurant coding and event identity (Critical)
**Evidence:** Raw rows can contain multiple violations from one event; IDs and inspection types are used as an event proxy.
**Action:** Standardize cuisine taxonomy, inspection event identifiers and contradictory grade/score observations; reconcile with source dictionary.
**Measure:** Zero unresolved duplicate-event or contradictory-grade exceptions.

## 7. Report time trends with comparable coverage (High)
**Evidence:** Extract dates range from **1900-01-01 00:00:00** to **2025-09-16 00:00:00**.
**Action:** Compare complete year periods and consistent inspection categories; exclude incomplete years from trend claims.
**Measure:** Year-over-year critical-event share with consistent definitions and confidence intervals where appropriate.

## Implementation roadmap
**0–30 days:** Confirm extract coverage and source dictionary; audit event-key collisions; validate top violations.  
**30–90 days:** Run targeted training and geographic field reviews; evaluate inspector consistency.  
**Quarterly:** Monitor reinspection compliance, critical violations and grade completeness.

## Interpretation caveats
Higher violation score is worse. Critical counts are inspection-based, not population risk. More inspections may reflect enforcement targeting. Do not infer causation or use raw cuisine differences to stigmatize communities.
