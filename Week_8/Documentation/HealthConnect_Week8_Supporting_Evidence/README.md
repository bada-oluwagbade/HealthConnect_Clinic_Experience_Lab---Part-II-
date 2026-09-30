# HealthConnect Week 8 supporting evidence

Prepared for Bada Oluwagbade on 29 September 2026.

## Start here
Read HealthConnect_Week8_Evidence_Guide.docx. Extract this archive before running code. Open HealthConnect_Week8_Verification.ipynb in Jupyter, or run `python reproduce_analysis.py` from this folder. Install pandas, numpy, scipy and matplotlib in your own Python environment if needed. Jupyter is needed only for interactive notebook use.

## Evidence scope
Data and calculations are verified from the supplied original CSV. The original file remains under data/. The script produces a separate eligible analytical dataset, summary tables, checks, charts and results.json. Rates use Attended + No-Show except cancellation rate, which uses all source rows. Missing distance stays Unknown and does not remove appointments from headline KPIs. The source fingerprint is recorded in results.json.

The notebook includes executed outputs from the same Python code. Model arithmetic uses the confusion matrix reported in the Week 7 report, not row-level predictions. Tests do not establish dashboard behavior or completed model integration.

## Pending evidence
Complete dashboard_acceptance.csv with observed values and real screenshots. Complete integration_log.csv with actual final exchanges, dates, changes and evidence of use. Keep the 86-versus-39 missing-distance discrepancy open until source versions and transformations reconcile. Do not infer appointment IDs from a scoring index.

## Sources
HealthConnect_Appointment_Data.csv and HealthConnect_Data_Dictionary.xlsx; Wk5-HealthConnect Clinic Experience lab.ipynb; HealthConnect_Week7_Analytics_Testing_Report.pdf and Project_Summary.pdf dated 28 September 2026; HealthConnect_Week6_Cross_Track_Integration_Evidence.docx; AnalystLab Africa Week 8 assignment. The prior reports establish documented historical context, not a new final handoff.
