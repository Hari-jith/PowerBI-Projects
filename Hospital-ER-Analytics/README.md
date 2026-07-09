# 🏥 Hospital Emergency Room (ER) Analytics Dashboard

An interactive **Power BI** dashboard built to help hospital administrators monitor Emergency Room operations — patient volume, wait times, satisfaction, and department referrals — across **daily, monthly, and custom date-range** views, down to individual patient-level detail.

---

## 📌 Project Overview

Emergency Rooms generate large volumes of operational data every day. This dashboard turns raw ER visit records into actionable insights so hospital staff can spot bottlenecks, staffing gaps, and service-quality issues before they become bigger problems.

The report contains **3 pages**:

| Page | Purpose |
|---|---|
| **Monthly View** | Month-by-month breakdown of KPIs and trends, filterable by Year & Month |
| **Consolidated View** | Same set of metrics aggregated over a fully custom, user-selected date range |
| **Patient Details** | A flat, filterable grid of individual patient records for drill-down/troubleshooting |

---

## 🗂️ Repository Contents

```
├── Hospital_Analytics.pbix     # Power BI dashboard file
├── Hospital_ER_Data.csv        # Source dataset
└── README.md                   # This file
```

---

## 📊 Dataset

**File:** `Hospital_ER_Data.csv`
**Rows:** ~9,216 patient visit records

| Column | Description |
|---|---|
| `Patient Id` | Unique patient identifier |
| `Patient Admission Date` | Timestamp of ER admission |
| `Patient First Inital` | First initial of patient |
| `Patient Last Name` | Patient surname |
| `Patient Gender` | Recorded as `M` / `F` / `NC` in the raw file |
| `Patient Age` | Age in years |
| `Patient Race` | Race/ethnicity category |
| `Department Referral` | Department the patient was referred to (or `None`) |
| `Patient Admission Flag` | `TRUE`/`FALSE` — whether the patient was admitted |
| `Patient Satisfaction Score` | Patient-reported satisfaction score |
| `Patient Waittime` | Minutes waited before being seen |
| `Patients CM` | Supporting numeric field used for aggregations |

---

## 🧹 Data Preparation (Power Query / Data Model)

Before building the visuals, the following transformations were applied:

- **Custom "Patient Full Name" column** — concatenated from `Patient First Inital` + `Patient Last Name`.
- **Gender re-labelling** — recoded the raw `M`, `F`, `NC` values into their full, readable forms (`Male`, `Female`, `Not Classified`) for cleaner labels in charts and tooltips.
- **New Date Table** — a dedicated calendar table generated from `Patient Admission Date`, from which `Year`, `Month`, `Day`, `Day Name`, and a `Date Hierarchy` (Year → Quarter → Month → Day) were extracted. This table drives all time-intelligence slicers and trend charts and is related to the main fact table on the date key.
- **Supporting calculated columns/measures** built on top of the fact table to power the KPIs and charts below, including patient counts, average wait time, referral counts, an age-bucketed `Age Group` field (10-year bands), and a `WaitTime Status` flag (seen within 30 minutes vs. not).

---

## 📈 Key Metrics (KPI Cards + Sparklines)

Four headline KPIs sit at the top of both the **Monthly View** and **Consolidated View** pages, each shown as a card with an **area sparkline** underneath to visualize the daily trend:

### 1. Number of Patients
Total count of ER patients. The daily area sparkline reveals peak days, week-over-week patterns, and any seasonal surges in ER traffic.

### 2. Average Wait Time
Average number of minutes a patient waits before being seen by a medical professional. The sparkline highlights days with unusually high wait times that may signal understaffing or capacity issues.

### 3. Patient Satisfaction Score
Average patient-reported satisfaction, tracked daily. The sparkline is used to spot dips in satisfaction and correlate them with high-volume or high-wait-time days.

### 4. Number of Patients Referred
Daily count of patients referred out of the ER to a specific department (Cardiology, Orthopedics, Neurology, General Practice, Physiotherapy, Gastroenterology, Renal, etc.). The sparkline tracks referral volume trends and helps flag departments that may need additional resourcing.

---

## 📄 Dashboard 1 — Monthly View

**Objective:** Monitor key metrics and trends on a month-by-month basis.

Includes:
- KPI cards + area sparklines (Patients, Wait Time, Satisfaction, Referrals)
- Year and Month slicers for quick navigation between periods
- **Patient Admission Status** — pivot table comparing admitted vs. non-admitted patient counts and % of total, plus a supporting bar chart
- **Patient Age Distribution** — clustered column chart grouping patients into 10-year age bands
- **Department Referrals** — clustered bar chart of referral volume by department
- **% of Patients Seen Within 30 Minutes** — donut chart measuring service timeliness
- **Patients by Gender** — donut chart showing gender split (Male / Female / Not Classified)
- **Patients by Race** — clustered bar chart of racial demographics
- **Patients by Day & Hour** — column chart plus a matrix (pivot table) breaking down patient volume and wait-time interval by day of week and hour, to spot peak traffic windows

---

## 📄 Dashboard 2 — Consolidated View

**Objective:** Provide a holistic summary of ER performance for a user-selected date range, rather than a fixed month.

Mirrors the **same chart set as the Monthly View** (admission status, age distribution, department referrals, timeliness, gender, race, day/hour analysis) — but every visual is driven by a **custom date-range slicer** (based on the Date Table) instead of Year/Month filters, enabling broader, flexible trend analysis across any period the user chooses.

---

## 📄 Dashboard 3 — Patient Details

**Objective:** Offer granular, patient-level data for detailed analysis and troubleshooting.

A single detail grid (table) with a date-range slicer, showing:

- Patient ID
- Patient Full Name
- Gender
- Age
- Admission Date
- Patient Race
- Wait Time
- Department Referral
- Admission Status

This page lets analysts drill into individual records behind any trend or anomaly spotted on the other two pages.

---

## 🛠️ Tools Used

- **Power BI Desktop** — data modeling, DAX measures, and report/dashboard design
- **Power Query** — data cleaning and transformation (custom columns, date table, gender relabeling)

---

## 🚀 How to Use

1. Download `Hospital_Analytics.pbix` and `Hospital_ER_Data.csv` from this repository (keep them in the same folder).
2. Open `Hospital_Analytics.pbix` in **Power BI Desktop** (free download from Microsoft).
3. If prompted, update the data source path to point to your local copy of `Hospital_ER_Data.csv`.
4. Use the **page navigator** on the left to switch between **Monthly View**, **Consolidated View**, and **Patient Details**.
5. Use the slicers (Year/Month or Date Range) at the top of each page to filter the analysis.

---

## ✅ Requirements Checklist

- [x] Number of Patients — daily trend, area sparkline
- [x] Average Wait Time — daily trend, area sparkline
- [x] Patient Satisfaction Score — daily trend, area sparkline
- [x] Number of Patients Referred — daily trend, area sparkline
- [x] Dashboard 1: Monthly View (Admission Status, Age Distribution, Department Referrals, Timeliness, Gender, Race, Day/Hour analysis)
- [x] Dashboard 2: Consolidated View (same metrics, custom date range)
- [x] Dashboard 3: Patient Details (full patient-level grid)
- [x] Custom "Patient Full Name" column
- [x] Gender values recoded to full form
- [x] New Date Table with extracted Month/Day

---

## 📷 Screenshots

> Add screenshots of each dashboard page here once uploaded, e.g.:
>
> ![Monthly View](Hospital-ER-Analytics/Images/monthly-view.png)
> ![Consolidated View](Hospital-ER-Analytics/Images/consolidated-view.png)
> ![Patient Details](Hospital-ER-Analytics/Images/patient-details.png)

