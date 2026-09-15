# HealthConnect Clinic Experience Lab

## Project overview
HealthConnect Clinic is a fictional appointment-based healthcare provider seeking to reduce missed appointments, improve appointment-slot utilisation and strengthen patient support using data and AI.

**Central question:**  
How can HealthConnect Clinic use data and AI to reduce missed appointments and improve the patient support experience?

## My track
**Data Analytics**

My role is to analyse appointment attendance patterns, validate business KPIs, identify high-impact operational segments and translate findings into practical decision support.

## Project progression

### Week 4 — Problem understanding
- Reviewed the dataset and data dictionary
- Assessed data quality
- Defined business questions and potential KPIs
- Established the initial analysis approach

### Week 5 — Exploratory analysis & dashboard
- Prepared and validated the appointment data
- Defined the eligible no-show population as Attended + No-Show
- Calculated five core KPIs
- Conducted EDA across patient history, reminders, lead time, distance, timing and appointment type
- Built an initial Power BI dashboard
- Identified previous no-show history, lead time and distance as the strongest descriptive patterns

### Week 6 — Advanced analytics, integration & validation
Week 6 moved from descriptive EDA to deeper decision-support analysis.

#### Key validated findings
- Overall no-show rate: **51.15%**
- Booking lead time: **29.5%** no-show rate at 0–7 days vs **68.5%** at 41–60 days
- Any previous no-show: **57.8%** vs **46.3%** without previous no-shows
- 2+ previous no-shows: **63.5%**
- 41–60 day lead time + 2+ previous no-shows: **83.3%**
- 20+ km distance: **60.2%**
- No reminder: **54.6%** vs **49.9%** with reminder
- Follow-up appointment: **54.2%**

#### Cross-track integration
I collaborated with the Data Science track by:
- providing validated segment findings for feature refinement and error analysis;
- receiving model feature/importance information, Logistic Regression coefficients and model scoring output;
- testing whether model-related factors were also meaningful in the appointment data;
- translating probability scores and model metrics into stakeholder-friendly dashboard content.

The supplied Logistic Regression scoring output produced approximately:
- Accuracy: **63.6%**
- Precision: **63.0%**
- Recall: **65.8%**
- F1: **64.4%**
- ROC-AUC: **68.9%**

A key integration issue was identified: the scoring export does not preserve the original `HC-xxxxx` appointment ID, so row-level model errors cannot yet be joined safely to the operational data.

## Week 6 deliverables
- `HealthConnect_Week6_Advanced_Analytics.ipynb`
- `HealthConnect_Week6_Advanced_Analytics_Report.docx`
- `HealthConnect_Week6_Project_Summary.docx`
- `HealthConnect_Week6_Cross_Track_Integration_Evidence.docx`
- `HealthConnect_Week6_Dashboard_Inputs.xlsx`
- `HealthConnect_Week6_Dashboard_Update_Guide.md`

## Tools
- Python
- Pandas
- Matplotlib
- SciPy
- Scikit-learn metrics
- Power BI
- Excel

## Limitations
- The dataset is fictional and anonymised.
- Findings are observational and do not establish causality.
- Reminder assignment may not be random.
- Model outputs from different collaborators may use different evaluation configurations.
- Final operational probability thresholds require clinic cost/capacity input.
- The current scoring export requires corrected identifiers before row-level integration.

## Week 7 focus
- Obtain model scores with true appointment and patient identifiers
- Analyse false positives and false negatives by operational segment
- Validate dashboard calculations and interactions
- Support threshold selection using business cost/capacity assumptions
- Test the stability of the highest-priority no-show segments

## Portfolio takeaway
The project demonstrates how descriptive analytics and predictive modelling can complement each other: Analytics identifies and explains operational patterns, while Data Science tests whether those patterns contribute to prediction. Week 6 connects both perspectives into a more practical decision-support workflow.
