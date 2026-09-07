# HealthConnect Clinic Appointment Analytics

![Python](https://img.shields.io/badge/Python-Data%20Analysis-blue)
![Power BI](https://img.shields.io/badge/Power%20BI-Dashboard-yellow)
![Project](https://img.shields.io/badge/Project-Healthcare%20Analytics-lightgrey)

## Project Overview

Missed appointments are more than empty spaces on a clinic calendar. They can reduce appointment-slot utilisation, make scheduling less efficient, and affect how effectively a healthcare provider serves patients.

This project analyses appointment attendance and no-show patterns for **HealthConnect Clinic**, a fictional healthcare provider used in the **AnalystLab Africa Experience Lab**.

The work began in **Week 4** with business understanding, dataset review, data-quality assessment, business-question development, and KPI planning. In **Week 5**, I moved from planning into practical implementation by preparing the data, conducting exploratory data analysis, calculating KPIs, identifying important no-show patterns, translating findings into business recommendations, and building a Power BI dashboard for decision-makers.

The central analytical question is:

> **What patterns are associated with appointment no-shows, and how can HealthConnect use these insights to improve appointment attendance and appointment-slot utilisation?**

---

## Business Problem

HealthConnect Clinic is experiencing operational challenges related to missed appointments.

The analysis focuses on understanding:

- how frequently eligible appointments are missed;
- whether previous missed appointments are associated with future no-shows;
- whether reminder activity is associated with attendance;
- whether booking lead time is associated with no-show behaviour;
- whether distance to the clinic is associated with missed appointments;
- whether no-show rates vary by appointment type, day, time, or patient age group;
- which appointment segments should receive greater operational attention.

The project is **descriptive and diagnostic**, not causal. Relationships identified in the data are treated as associations rather than proof that one factor causes another.

---

## Project Objectives

The Week 5 analysis was designed to:

1. Prepare and validate the HealthConnect appointment dataset.
2. Define an appropriate analytical population for no-show analysis.
3. Calculate and interpret business-relevant KPIs.
4. Conduct exploratory analysis across patient and appointment characteristics.
5. Identify segments with comparatively higher observed no-show rates.
6. Translate analytical findings into practical business recommendations.
7. Present the findings in a clear Power BI dashboard for healthcare administrators and decision-makers.
8. Create a reusable project structure suitable for a professional analytics portfolio.

---

## Dataset

The dataset contains **5,000 fictional and anonymised appointment records** covering appointments from **January 2025 to June 2026**.

### Dataset Summary

| Metric | Value |
|---|---:|
| Total appointment records | 5,000 |
| Unique patients | 1,696 |
| Attended appointments | 2,314 |
| No-show appointments | 2,423 |
| Cancelled appointments | 263 |
| Eligible attendance appointments | 4,737 |
| Overall no-show rate | 51.2% |
| Cancellation rate | 5.26% |

### Available Variables

The dataset includes:

- `appointment_id`
- `patient_id`
- `gender`
- `age`
- `age_group`
- `appointment_type`
- `booking_date`
- `appointment_date`
- `appointment_day`
- `appointment_time`
- `booking_lead_days`
- `previous_appointments`
- `previous_no_shows`
- `reminder_sent`
- `reminder_channel`
- `distance_to_clinic_km`
- `waiting_time_minutes`
- `appointment_outcome`

Appointment outcomes are recorded as:

- **Attended**
- **No-Show**
- **Cancelled**

---

## Tools Used

### Analysis
- **Python**
- **Pandas**
- **NumPy**
- **Matplotlib**
- **Jupyter Notebook**

### Dashboard & Business Intelligence
- **Power BI**
- **DAX**

### Documentation & Version Control
- **Git**
- **GitHub**
- **Markdown**

---

## Project Workflow

The analytical workflow followed this structure:

```text
Business Understanding
        ↓
Data & Dictionary Review
        ↓
Data Quality Assessment
        ↓
Data Preparation
        ↓
Analytical Population Definition
        ↓
KPI Development
        ↓
Exploratory Data Analysis
        ↓
Business Insights
        ↓
Power BI Dashboard
        ↓
Recommendations & Documentation
```

---

## Data Quality Assessment

Before calculating KPIs, I reviewed the dataset for missing values, duplicates, data types, categorical consistency, and logical relationships.

### Duplicate Checks

- Duplicate rows: **0**
- Duplicate appointment IDs: **0**

`appointment_id` was therefore retained as the unique appointment identifier.

### Missing Values

| Variable | Missing Records | Percentage |
|---|---:|---:|
| `reminder_channel` | 1,366 | 27.32% |
| `distance_to_clinic_km` | 90 | 1.80% |
| `waiting_time_minutes` | 60 | 1.20% |

### Important Missing-Data Decision

The missing values in `reminder_channel` were not automatically treated as data-quality errors.

Further inspection showed that the same appointments had:

```text
reminder_sent = "No"
```

The data dictionary indicates that the reminder channel should be empty when no reminder was sent. These blanks were therefore treated as **structurally expected missing values** rather than incomplete records.

For `distance_to_clinic_km` and `waiting_time_minutes`, records were retained in the main dataset and excluded only from analyses that required the missing variable.

This preserved usable information in the remaining fields instead of deleting complete appointment records unnecessarily.

---

## Analytical Population

One of the most important methodological decisions was how to treat cancelled appointments.

A cancellation is operationally different from a patient failing to attend. Therefore, cancelled appointments were retained for operational reporting but excluded from the denominator of the main no-show KPI.

### Eligible Attendance Population

```text
Eligible Appointments = Attended + No-Show
```

```text
Eligible Appointments = 2,314 + 2,423 = 4,737
```

---

## KPI Definitions

### 1. Overall No-Show Rate

**Business Question:** How frequently are eligible appointments missed?

```text
No-Show Rate =
No-Shows / (Attended + No-Shows)
```

```text
2,423 / 4,737 = 51.2%
```

**Result:** **51.2%**

This establishes the baseline size of the appointment-attendance problem.

---

### 2. No-Show Rate by Previous No-Show History

**Business Question:** Are previous missed appointments associated with current attendance?

| Previous History | No-Show Rate |
|---|---:|
| No previous no-show | 46.3% |
| Previous no-show | 57.8% |

Patients with previous missed appointments showed a higher observed no-show rate.

---

### 3. No-Show Rate by Reminder Status

**Business Question:** Are reminders associated with different attendance behaviour?

| Reminder Status | No-Show Rate |
|---|---:|
| Reminder sent | 49.9% |
| No reminder | 54.6% |

Appointments with reminders recorded a lower observed no-show rate than appointments without reminders.

This is an association and does not by itself prove that reminders caused the difference.

---

### 4. No-Show Rate by Booking Lead Time

**Business Question:** Does the time between booking and appointment matter?

| Booking Lead Time | No-Show Rate |
|---|---:|
| 0–7 days | 29.5% |
| 8–14 days | 35.2% |
| 15–30 days | 45.5% |
| 31–60 days | 63.9% |

Booking lead time showed the clearest ordered pattern in the analysis: the observed no-show rate increased as appointments were scheduled further in advance.

---

### 5. No-Show Rate by Distance to Clinic

**Business Question:** Is travel distance associated with missed appointments?

| Distance | No-Show Rate |
|---|---:|
| 0–5 km | 48.7% |
| 5–10 km | 49.3% |
| 10–20 km | 52.3% |
| 20+ km | 60.5% |

The 20+ km group recorded the highest observed no-show rate.

---

## Exploratory Data Analysis

Beyond the core KPIs, I explored no-show patterns across additional appointment and patient characteristics.

### Appointment Type

| Appointment Type | No-Show Rate |
|---|---:|
| Follow-up | 54.2% |
| Diagnostic Test | 52.0% |
| Specialist Consultation | 50.5% |
| General Consultation | 49.1% |

Follow-up appointments had the highest observed no-show rate among appointment types.

### Appointment Day

| Day | No-Show Rate |
|---|---:|
| Monday | 53.1% |
| Sunday | 52.8% |
| Wednesday | 52.8% |
| Thursday | 52.0% |
| Saturday | 49.6% |
| Tuesday | 48.9% |
| Friday | 48.7% |

The differences by day were smaller than those observed for booking lead time or distance.

### Appointment Time

| Appointment Time | No-Show Rate |
|---|---:|
| Morning | 50.7% |
| Afternoon | 51.2% |
| Evening | 52.6% |

Appointment time showed only a modest difference across periods.

### Age Group

| Age Group | No-Show Rate |
|---|---:|
| 55–64 | 53.0% |
| 25–34 | 52.9% |
| 18–24 | 52.4% |
| 35–44 | 51.4% |
| 45–54 | 51.1% |
| 65+ | 48.1% |

Age-group differences were relatively small compared with the strongest operational variables.

---

## Key Findings

### 1. The overall no-show baseline is high

**51.2%** of eligible appointment opportunities resulted in a no-show.

This suggests that missed appointments represent a substantial operational issue in the dataset.

### 2. Booking lead time produced the strongest ordered pattern

No-show rates rose from **29.5%** for appointments booked within 0–7 days to **63.9%** for appointments booked 31–60 days ahead.

This suggests long-lead appointments may deserve additional confirmation or engagement closer to the appointment date.

### 3. Previous no-show history is an important segmentation signal

Patients with previous no-shows had an observed no-show rate of **57.8%**, compared with **46.3%** among those with no previous no-shows.

Historical appointment behaviour may therefore be useful for prioritising engagement.

### 4. Longer travel distance is associated with higher observed no-show rates

Patients travelling **20+ km** recorded a **60.5%** no-show rate.

Distance may therefore be relevant when considering appointment accessibility.

### 5. Reminder status is associated with attendance

Appointments with reminders had a **49.9%** no-show rate compared with **54.6%** where no reminder was sent.

The result supports further investigation of reminder coverage and reminder strategy.

### 6. Follow-up appointments deserve attention

Follow-up appointments recorded an observed no-show rate of **54.2%**, the highest among appointment types.

---

## Priority Segments

The Power BI dashboard summarises the segments with comparatively higher observed no-show rates.

| Priority Segment | Priority | Observed No-Show Rate |
|---|---|---:|
| Lead time: 31–60 days | High | 63.9% |
| Distance: 20+ km | High | 60.5% |
| Previous no-show history | High | 57.8% |
| No reminder sent | Moderate | 54.6% |
| Follow-up appointment | Moderate | 54.2% |
| Monday appointments | Moderate | 53.1% |

> **Important:** These are analytical priority segments based on descriptive results. They are **not predictive patient-risk scores**.

---

## Power BI Dashboard

The Week 5 Power BI dashboard was designed to give healthcare administrators a quick view of appointment performance, time trends, important no-show patterns, and priority segments.

### Dashboard Components

The dashboard includes:

- Total Appointments
- Total No-Shows
- Overall No-Show Rate
- Attended Appointments
- Cancelled Appointments
- Cancellation Rate
- Unique Patients
- Monthly No-Show Rate
- Appointment Outcomes Over Time
- No-Show Rate by Reminder Status
- No-Show Rate by Booking Lead Time
- Previous No-Show History
- Appointment Time
- Appointment Type
- Age Group
- Day of Week
- Key Insights
- Priority Segments

## Power BI Measures

Examples of measures used in the dashboard include:

```DAX
Total Appointments =
COUNTROWS(Appointments)
```

```DAX
Total No-Shows =
CALCULATE(
    COUNTROWS(Appointments),
    Appointments[appointment_outcome] = "No-Show"
)
```

```DAX
Attended Appointments =
CALCULATE(
    COUNTROWS(Appointments),
    Appointments[appointment_outcome] = "Attended"
)
```

```DAX
Eligible Appointments =
[Total No-Shows] + [Attended Appointments]
```

```DAX
No-Show Rate =
DIVIDE(
    [Total No-Shows],
    [Eligible Appointments],
    0
)
```

```DAX
Cancelled Appointments =
CALCULATE(
    COUNTROWS(Appointments),
    Appointments[appointment_outcome] = "Cancelled"
)
```

```DAX
Cancellation Rate =
DIVIDE(
    [Cancelled Appointments],
    [Total Appointments],
    0
)
```

---

## Challenges & Problem-Solving

The project involved several analytical and technical challenges.

### 1. Understanding Missing Data

At first glance, `reminder_channel` appeared to contain a large amount of missing information.

Instead of immediately removing those records, I compared the field with `reminder_sent` and found that the blank channel values corresponded to appointments where no reminder had been sent.

**Lesson:** Missing values should be understood in their business context before they are cleaned.

### 2. Deciding How to Treat Cancellations

Including cancelled appointments in the no-show denominator would mix different appointment outcomes.

I therefore retained cancellations for operational reporting but calculated no-show rate only from:

```text
Attended + No-Show
```

**Lesson:** KPI definitions can materially change the story a dashboard tells.

### 3. Handling Missing Distance and Waiting-Time Values

Deleting every record containing a missing distance or waiting-time value would have removed appointments that were still valid for other analyses.

I therefore used analysis-specific exclusion instead of complete-case deletion.

**Lesson:** Data cleaning should preserve useful information wherever possible.

### 4. Translating Python Analysis into Power BI

The findings calculated during EDA had to remain consistent when recreated as DAX measures and dashboard visuals.

This required validating Power BI results against the notebook before formatting the dashboard.

**Lesson:** A dashboard should be the presentation layer of an analysis, not a separate version of the truth.

### 5. Power BI Sorting and Circular Dependencies

Creating ordered categories such as booking lead-time groups, day of week, and appointment time introduced circular-dependency errors in Power BI.

I resolved this by separating display/grouping fields from sort fields and deriving sort logic from the original source variables.

**Lesson:** Data modelling and DAX structure are just as important as visual design in Power BI.

### 6. Avoiding Dashboard Overload

The dataset contained many variables, but not all of them deserved equal visual importance.

Variables such as lead time, previous no-show history, distance, and reminders showed more useful patterns than some demographic variables.

**Lesson:** Good dashboard design requires prioritising the information most relevant to decision-making.

---

## Business Recommendations

Based on the observed patterns, HealthConnect could consider the following actions for testing and further evaluation:

### 1. Reconfirm Long-Lead Appointments

Appointments scheduled several weeks in advance showed substantially higher observed no-show rates.

HealthConnect could test an additional confirmation step closer to the appointment date for long-lead bookings.

### 2. Use Previous Appointment History for Targeted Engagement

Patients with previous missed appointments may benefit from additional confirmation or engagement before future appointments.

### 3. Review Reminder Coverage

Because appointments without reminders had a higher observed no-show rate, HealthConnect could review:

- whether all eligible appointments receive reminders;
- how far in advance reminders are sent;
- whether different reminder channels perform differently.

### 4. Investigate Distance-Related Access Barriers

The higher rate among patients travelling 20+ km suggests that accessibility may deserve further investigation.

Potential areas for future evaluation could include rescheduling flexibility, remote options where appropriate, or different appointment-support approaches.

### 5. Review Follow-Up Appointment Processes

Follow-up appointments showed a comparatively higher no-show rate.

The clinic could examine whether follow-up scheduling, reminder timing, or patient communication differs from other appointment types.

### 6. Monitor Changes Over Time

The monthly no-show trend should continue to be tracked so that future interventions can be evaluated against the current baseline.

---

## Limitations

This project has several important limitations.

### Synthetic Dataset

The HealthConnect dataset is fictional and anonymised. Findings demonstrate analytical methodology and should not be generalised directly to a real healthcare organisation.

### Association Does Not Equal Causation

The analysis identifies observed relationships.

For example:

- reminders are associated with a lower observed no-show rate;
- longer lead times are associated with a higher observed no-show rate.

These results do not prove that the variables caused the outcomes.

### Missing Data

Limited missing values exist in distance and waiting-time fields. Analyses using these variables therefore use only records with available values.

### Unobserved Factors

The dataset does not contain every factor that may influence appointment attendance, such as transportation availability, employment constraints, health status, socioeconomic circumstances, or patient communication preferences.

### No Predictive Risk Model

The Week 5 Data Analytics work identifies priority segments descriptively. It does not generate patient-level predictive risk scores.

---

## Project Deliverables

### Week 4

- Initial Analysis Notebook
- Dataset Overview
- Data Quality Assessment
- Business Questions
- Proposed KPIs
- Initial Analysis Approach
- Week 4 Project Summary

### Week 5

- Exploratory Analytics Notebook
- Cleaned/Processed Dataset
- KPI Calculations
- EDA Visualisations
- Power BI Dashboard
- Business Analytics Report
- Week 5 Project Summary
- Updated GitHub Repository

---

## Repository Structure

```text
healthconnect-appointment-analytics/
│
├── README.md
│
├── data/
│   ├── raw/
│       └── HealthConnect_Appointment_Data
|
│   └── processed/
│       └── HealthConnect_Appointment_Data_Cleaned.csv
│
├── notebooks/
│   ├── 01_HealthConnect_Week4_Initial_Analysis.ipynb
│   └── 02_HealthConnect_Week5_EDA.ipynb
│
├── dashboard/
│   ├── HealthConnect_Week5_Dashboard.pbix
│   └── HealthConnect_Week5_Dashboard.pdf
│
├── reports/
│   ├── HealthConnect_Week5_Business_Report.pdf
│   └── HealthConnect_Week5_Project_Summary.pdf
│
├── images/
│   └── healthconnect_dashboard_preview.png
│
└── docs/
    └── data_cleaning_log.md
```

> The original internship-provided dataset should only be included publicly if redistribution is permitted. Otherwise, keep it out of the public repository and explain this in `data/raw/README.md`.

---

## Project Progress

### Week 4 — Problem Understanding & Analysis Planning

Week 4 established the analytical foundation by:

- understanding the HealthConnect business problem;
- reviewing the dataset and data dictionary;
- assessing initial data quality;
- defining business questions;
- proposing KPIs;
- identifying assumptions and limitations;
- developing the Week 5 analytical approach.

### Week 5 — Exploratory Analysis & Initial Implementation

Week 5 moved the project into practical implementation by:

- preparing and validating the appointment data;
- defining the analytical population;
- calculating KPIs;
- conducting EDA;
- identifying priority segments;
- creating business recommendations;
- developing the Power BI dashboard;
- documenting challenges and analytical decisions.

---

## Next Steps

The next phase of the project can focus on:

- refining dashboard usability and interactivity;
- validating findings with additional analysis;
- examining combinations of multiple no-show factors;
- investigating reminder channels in more detail;
- exploring interactions between lead time, previous history, and appointment type;
- comparing segment volume as well as no-show rate;
- supporting future predictive modelling work where appropriate;
- developing the final HealthConnect project presentation.

---

## Key Learning

The most important lesson from this stage of the project was that analytics is not simply about creating charts.

The work required:

- understanding what the data represents;
- defining metrics carefully;
- making defensible cleaning decisions;
- validating calculations across tools;
- troubleshooting data-model issues;
- deciding which findings deserve attention;
- and communicating the results in a way that supports decision-making.

A technically correct result is only useful when its meaning is also clear.

---

## Author

**Gbade Bada**

Data & Business Analytics | Python | SQL | Power BI | GIS

---

## Programme

This project was developed as part of the **AnalystLab Africa Experience Lab Internship Programme** under the **HealthConnect Clinic Experience Lab**.

Project theme:

> **Improving Patient Appointment Attendance and Healthcare Support Using Data and AI**

---

## Disclaimer

HealthConnect Clinic and the appointment dataset used in this project are fictional and were created for learning and portfolio development.

The analysis does not provide medical advice and should not be interpreted as an assessment of a real healthcare organisation.

---

## Tags

`Data Analytics` `Business Analytics` `Healthcare Analytics` `Python` `Pandas` `Power BI` `DAX` `Data Visualization` `Exploratory Data Analysis` `KPI Development`

---

## Connect

If you found this project useful or would like to discuss analytics, business intelligence, or data storytelling, feel free to connect with me on LinkedIn.

