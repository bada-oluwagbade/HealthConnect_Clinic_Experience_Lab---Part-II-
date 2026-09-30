# HealthConnect Clinic Experience Lab

## Appointment Attendance Analysis and Decision Support

**Bada Oluwagbade · Data Analytics Track · AnalystLab Africa Experience Lab**  
**Project period: Weeks 4–8**  
**Documentation updated: 30 September 2026**

How can a clinic decide where to focus its support when more than half of eligible appointments are missed?

That question guided my work on HealthConnect. Over five weeks, I reviewed appointment data, developed KPIs and a Power BI dashboard, explored attendance patterns, collaborated with Data Science, and checked the evidence behind my recommendations.

The final analysis identified booking lead time and previous attendance history as useful priorities for testing supportive outreach. It also reinforced an important lesson: a high percentage needs context, including the size of the group, its share of the overall problem, and the limits of the evidence.

> **Project context:** HealthConnect is a fictional clinic. The supplied data are synthetic and anonymised. Findings describe this project dataset; they do not establish real-clinic performance or demonstrate that an intervention reduced no-shows.

## Project at a glance

| Item | Summary |
|---|---|
| Business question | How can data and AI support better appointment attendance and patient support? |
| My responsibility | Analyse attendance patterns, validate KPIs, communicate findings and propose operational actions |
| Source data | 5,000 appointments, 18 fields and 1,696 distinct patient IDs |
| Appointment dates | 1 January 2025–30 June 2026 |
| Analytical population | 4,737 attended or no-show appointments |
| Baseline no-show rate | **51.15%**, representing 2,423 missed appointments |
| Core tools | Python, pandas, NumPy, Matplotlib, SciPy, Jupyter Notebook and Power BI |
| Main outputs | Analysis notebooks, dashboard, validation evidence, final report and stakeholder presentation |
| Current position | Descriptive analytics prepared; dashboard acceptance and final integration evidence remain incomplete |

## The business problem

Missed appointments can leave slots unused and make scheduling less predictable. HealthConnect also wants to improve patient communication and administrative support.

My analysis focused on questions that could guide operational decisions:

- How often are appointments missed, attended or cancelled?
- How does attendance vary with booking lead time and previous no-show history?
- What differences appear across reminder status, appointment type, distance and appointment timing?
- Which groups combine a high no-show rate with a meaningful number of appointments?
- Which recommendations are supported by the findings, and what still needs testing?

My contribution covers **Data Analytics**. Model development, scoring infrastructure and the GenAI assistant belong to their respective tracks.

## My journey from Week 4 to Week 8

| Week | Focus | My work and progression |
|---|---|---|
| **4** | Problem understanding and initial assessment | Reviewed the business scenario and data dictionary, inspected the dataset, checked missing values and identifiers, and defined business questions, potential KPIs and an analysis approach. |
| **5** | Exploratory analysis and dashboard development | Prepared a working dataset, calculated attendance KPIs, compared patient and appointment segments, and developed a Power BI dashboard to communicate the patterns. |
| **6** | Deeper analysis and cross-track collaboration | Refined the lead-time groups, explored combinations of lead time and attendance history, assessed exploratory associations, and exchanged findings and model-related information with Data Science. |
| **7** | Testing and refinement | Rechecked KPIs and segment results, reviewed shared definitions and available model evidence, and documented dashboard, missing-distance and prediction-ID issues. |
| **8** | Final reporting and stakeholder communication | Consolidated the analytical report and reproducible evidence package, prepared an editable stakeholder presentation with speaker notes, and translated findings into a proposed pilot and readiness actions. |

The work built forward each week. Earlier exploratory outputs remain useful as a record of the process, while the final report provides the consolidated definitions and findings.

## Data preparation and calculation rules

The original dataset remains unchanged. Cleaning and derived features belong in separate working files.

### Appointment outcomes

| Outcome | Appointments |
|---|---:|
| Attended | 2,314 |
| No-Show | 2,423 |
| Cancelled | 263 |
| **Total** | **5,000** |

The main no-show denominator excludes cancellations:

```text
Eligible appointments = Attended + No-Show
                      = 2,314 + 2,423 = 4,737

No-show rate = No-Show / Eligible appointments × 100
             = 2,423 / 4,737 × 100 = 51.15%
```

Attendance is **48.85%** of eligible appointments. Cancellation is **5.26%** of all 5,000 appointments. These rates use different denominators and should not be combined indiscriminately.

### Important preparation decisions

- Used `appointment_id` to identify appointments. Repeated `patient_id` values represent legitimate repeat visits and are not automatically duplicates.
- Checked date parsing and agreement between booking dates, appointment dates and `booking_lead_days`.
- Checked that historical no-shows do not exceed historical appointments.
- Treated the absence of a reminder channel when no reminder was sent as an expected condition.
- Used final inclusive lead-time bands of **0–7, 8–21, 22–40 and 41–60 days**. Some early Week 5 comparisons used different bands; their rates are not directly interchangeable with the final groups.
- Defined high previous no-show history as **at least two previous no-shows**.
- Calculated previous no-show rate as `previous_no_shows / previous_appointments`, using zero where no previous appointment exists and retaining a separate no-history flag in the final evidence.
- Kept missing distance as **Unknown** in the final descriptive analysis, without removing those appointments from the headline KPI.
- Excluded waiting time from the proposed prioritisation rule because its availability before attendance is unclear.

## What the analysis revealed

### 1. Longer lead time is associated with a higher no-show rate

| Booking lead time | Appointments | No-shows | No-show rate |
|---|---:|---:|---:|
| 0–7 days | 604 | 178 | 29.47% |
| 8–21 days | 1,148 | 448 | 39.02% |
| 22–40 days | 1,484 | 769 | 51.82% |
| 41–60 days | 1,501 | 1,028 | 68.49% |

The longest-lead group accounts for **42.43% of all no-shows**. It matters because of both its rate and its volume.

**Decision implication:** test reconfirmation closer to the appointment date for bookings made far ahead, with a clear route to confirm, cancel or reschedule.

### 2. Attendance history identifies a smaller group for extra support

Appointments booked **41–60 days ahead**, with **two or more previous no-shows**, recorded:

- **156 appointments** and **130 no-shows**.
- An **83.33% no-show rate**.
- **5.37% of all no-shows** in the eligible population.

This group could help prioritise extra contact when staff capacity is limited. However, focusing only on it would leave most missed appointments outside the intervention.

The 83.33% figure is a historical group rate, not an individual model prediction.

### 3. Reminder differences are worth testing

| Reminder status | Appointments | No-shows | No-show rate |
|---|---:|---:|---:|
| No reminder | 1,285 | 702 | 54.63% |
| Reminder sent | 3,452 | 1,721 | 49.86% |

The difference is **4.78 percentage points**, calculated before rounding. Other characteristics may influence both reminder assignment and attendance, so this comparison does not prove that reminders caused better attendance.

**Decision implication:** compare a defined reminder change with usual practice in a controlled pilot.

### 4. Statistical results need context

Exploratory categorical comparisons gave lead time the largest association among the variables tested: **Cramér’s V ≈ 0.276**, compared with **0.122** for previous no-show history and approximately **0.042** for reminder status and appointment type.

These appointment-level analyses do not adjust for repeated patients and do not establish causality. I used them to support investigation and interpretation, rather than claim a confirmed intervention effect.

## Cross-track collaboration

The documented exchange was with **Data Science**.

| Direction | Exchange | Effect on my work |
|---|---|---|
| Received from Data Science | Model-related outputs, feature information, scoring results and shared definitions | Helped align the lead-time groups and focus the investigation on lead time and attendance history |
| Provided to Data Science | Validated appointment patterns, segment comparisons and business interpretations | Supplied descriptive evidence for comparison with modelling results |
| Integration issue identified | Scoring output lacked a verified `appointment_id` | Prevented a reliable appointment-level join and created a clear follow-up requirement |

Agreement on the **4,737-row population count** does not, by itself, confirm identical record membership or preprocessing. Predictions should not be joined to appointments by assumed row order.

The final report and presentation describe how Analytics connects to Data Science, ML Engineering, GenAI and Project Management. Final handoff acceptance and evidence that other tracks used the Week 8 package remain pending.

## Recommendations for HealthConnect

These actions are **proposals for evaluation**, not implemented outcomes.

| Proposed action | Suggested owner | What to measure |
|---|---|---|
| Reconfirm bookings made 41–60 days ahead | Scheduling team | No-show rate, confirmations and timely cancellations |
| Offer extra support within that group where there are 2+ previous no-shows | Patient support | Attendance, successful contacts and staff minutes |
| Test a specified reminder change against usual practice | Operations with Analytics | Difference in no-show rates, delivery success and outreach effort |
| Review consistent appointment KPIs | Analytics with Project Management | Eligible volume, attendance, no-shows and cancellations |

A **proposed four-week pilot** provides a starting point. Before launch, the team should agree capacity, a comparison group, success criteria and the necessary readiness checks. Where feasible, assign patients rather than individual appointments to comparison groups to reduce crossover from repeat visits. Extend the evaluation if appointment volume is insufficient.

## Validation and current limitations

The final evidence package records **15 defined source-data checks** and reproduces the headline KPIs and main segments. This supports the descriptive analysis, but it does not certify dashboard behavior or model readiness.

| Area | Current status / next step |
|---|---|
| Source KPIs and main segment calculations | Reproduced from the original data |
| Final report, evidence package and presentation | Prepared |
| Dashboard acceptance | Record filter, sorting, reset and refresh tests |
| Missing-distance discrepancy | Reconcile 90 missing values in the full source, 86 among eligible appointments, and the reported working-notebook count of 39 |
| Prediction integration | Obtain stable appointment IDs and confirm matching record membership and preprocessing |
| Model decision threshold | Agree outreach capacity and error costs with the relevant owners; retain supporting validation evidence |
| Final team handoff and walkthrough | Document receipt, use, resulting changes and acceptance |
| Individual presentation recording | Slides and speaker notes prepared; completed recording is not evidenced here |

The synthetic data, repeated patients and observational design limit interpretation. No real-clinic attendance reduction, financial return, deployed system or completed intervention is claimed.

## Deliverables and where to start

Read the final report for the complete story, use the presentation for the stakeholder narrative, and consult the evidence archive to trace the calculations.

| Artifact | Purpose |
|---|---|
| `HealthConnect_Initial_Analysis.html` | Week 4 dataset review and initial analytical approach |
| `Wk5-HealthConnect Clinic Experience lab.ipynb` | Week 5 preparation, KPI calculations and exploratory analysis |
| `HealthConnect_Week5_Dashboard.pdf` | Export of the dashboard developed during Week 5 |
| Week 6 integration record and Week 7 testing documentation | Collaboration, shared definitions, tests and unresolved issues |
| `HealthConnect_Week8_Final_Report.docx` | Consolidated findings, recommendations and readiness assessment |
| `HealthConnect_Week8_Supporting_Evidence.zip` | Executed verification notebook, data, tables, charts, script and acceptance records |
| `HealthConnect_Week8_Evidence_Guide.docx` | Guide to the supporting evidence and remaining actions |
| `HealthConnect_Stakeholder_Final.pptx` | Editable final presentation with timed speaker notes |
| `HealthConnect_Stakeholder_Presentation.pdf` | PDF copy of the stakeholder slides |
| `HealthConnect_Presenter_Preparation.pdf` | Rehearsal guidance and stakeholder questions with answers |

These filenames describe project artifacts. Their availability in a GitHub checkout depends on which files have been uploaded to that repository.

### Suggested repository organisation

| Folder | Contents |
|---|---|
| `data/raw/` | Original CSV and data dictionary |
| `week4/` | Initial analysis and project summary |
| `week5/` | Exploratory notebook, dashboard and interpretation |
| `week6/` | Refined analysis and integration evidence |
| `week7/` | Testing notebook, results and issue records |
| `week8/` | Final report, presentation and preparation materials |
| `evidence/week8/` | Extracted Week 8 supporting evidence, preserving its internal folders |

## Reproducing the final analysis

1. Extract `HealthConnect_Week8_Supporting_Evidence.zip` into `evidence/week8/` or another dedicated directory.
2. Preserve the archive’s relative structure, including its `data/`, `tables/` and `figures/` folders.
3. Use a Python environment with `pandas`, `numpy`, `scipy` and `matplotlib`. Install Jupyter if you want to inspect or rerun the notebook. A locked dependency environment is not included.
4. From the extracted evidence directory, run:

```bash
python reproduce_analysis.py
```

5. Review `results.json`, the regenerated summary tables and `HealthConnect_Week8_Verification.ipynb`. The script regenerates derived outputs; keep a copy if you want to preserve the previously supplied evidence.
6. Confirm the main reference values: **5,000 source rows**, **4,737 eligible appointments**, **2,423 no-shows**, and **130/156** in the combined priority segment.

Earlier notebooks may contain machine-specific file paths. Update those paths to your local copies of the supplied data before running them. Use the final definitions above when comparing weekly outputs.

Power BI requires a separate review: refresh the data source and test dashboard interactions. Python checks alone do not validate the dashboard.

## What I learned

This project strengthened my ability to connect data preparation with business interpretation. I learned to check denominators before comparing rates, distinguish expected blanks from missing observations, and consider both the size and reach of a priority group.

Collaboration also showed me that matching a row count is not enough for integration. Shared definitions, stable identifiers and documented handoffs matter just as much as the analysis itself.

My next step would be to close the remaining readiness checks and evaluate whether the proposed support improves attendance without creating an unsustainable workload for clinic staff.

## Attribution

Project scenario, assignment briefs and source resources: **AnalystLab Africa Experience Lab**.  
Data Analytics contribution and portfolio documentation: **Bada Oluwagbade**.

This README summarises my work across Weeks 4–8. The final report and supporting evidence document the calculation rules and limitations behind the findings.
