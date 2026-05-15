# 🫀 Hypertension Cardiology Centre Analytics Report

**Improving Blood Pressure Control: Predictors and Treatment Optimization**

> A data analytics project examining blood pressure control outcomes, treatment effectiveness, and predictors of hypertension management failure across 350 patients in a 2024 cardiology cohort.

---

## 📋 Table of Contents

- [Project Overview](#project-overview)
- [Dataset](#dataset)
- [Key Findings](#key-findings)
- [Methodology](#methodology)
- [Feature Engineering](#feature-engineering)
- [Analysis Modules](#analysis-modules)
- [Results Summary](#results-summary)
- [Recommendations](#recommendations)
- [Glossary](#glossary)
- [Author](#author)

---

## Project Overview

This project analyses patient records from a Hypertension Cardiology Centre to answer two core clinical questions:

1. **What predicts blood pressure control failure at 3 months?**
2. **Which antihypertensive drug class delivers the best outcomes by comorbidity profile?**

The analysis covers medication adherence patterns, baseline BP severity, drug class performance, comorbidity burden, visit frequency, and age-stratified control rates — producing actionable recommendations for clinical treatment optimization.

---

## Dataset

| Attribute | Detail |
|---|---|
| **Source** | Hypertension Cardiology Centre Records |
| **Cohort Year** | 2024 |
| **Total Records** | 350 patient entries |
| **Original Variables** | 16 columns |
| **Engineered Features** | 4 additional columns |
| **Total Features (post-processing)** | 20 columns |
| **Duplicates** | 0 — dataset is clean |
| **Age Range** | 30–85 years (mean: 57.4 yrs) |
| **Gender Split** | Male: 172 (49%) / Female: 178 (51%) |

---

## Key Findings

### Overall BP Control Rate
- **9.4%** of patients (33 of 350) achieved controlled BP at 3 months
- **90.6%** remained uncontrolled at the 3-month mark

### Top Predictors of BP Control Failure

| Rank | Predictor | Impact |
|---|---|---|
| 1 | Medication Adherence | 8× control gap between good and poor adherers |
| 2 | BP Stage at Prescription | Hypertensive Crisis → 0% control across ALL drug classes |
| 3 | Drug Class Selection | Combination Therapy achieved 21.1% — only class above 13% |
| 4 | Visit Frequency | ≤1 visit: 5.3% control vs 2 visits: 15.9% control |

### Drug Class Performance

| Drug Class | Control Rate | Patients |
|---|---|---|
| Combination Therapy | **21.1%** ✅ | 57 |
| Thiazide Diuretic | 13.1% | 61 |
| Beta Blocker | ~9.8% | 61 |
| ARB | ~6.0% | 68 |
| Calcium Channel Blocker | ~5.2% | 58 |
| ACE Inhibitor | **0%** ❌ | 45 |

### Comorbidity Prevalence (of 350 patients)

| Comorbidity | Count | Prevalence |
|---|---|---|
| Obesity | 186 | 53% |
| Diabetes Mellitus | 182 | 52% |
| CKD | 182 | 52% |
| Dyslipidemia | 163 | 47% |

---

## Methodology

The analysis pipeline includes:

1. **Data Cleaning** — duplicate check, null handling, type validation
2. **Feature Engineering** — 4 new variables derived from raw data (see below)
3. **Exploratory Data Analysis (EDA)** — distribution plots, correlation matrices, group comparisons
4. **Outcome Analysis** — BP control rates segmented by adherence, drug class, BP stage, age group, and comorbidity profile
5. **Drug × Comorbidity Cross-tabulation** — control success and failure rates by drug class against comorbidity count (0–4)
6. **BP Stage Transition Analysis** — before-to-after medication BP classification tracking

---

## Feature Engineering

Four features were engineered from the original 16 variables:

### 1. Age Group
Continuous age was binned into four clinical categories:
- Under 45
- 46–55
- 56–65
- 66+

### 2. Comorbidity Rate
A burden score (0–4) counting the number of active comorbidities per patient across four lab-tested conditions:
- `0` — All lab tests negative
- `1` — One positive
- `2` — Two positive
- `3` — Three positive
- `4` — All four positive (Diabetes, CKD, Dyslipidemia, Obesity)

### 3. BP Level Before Prescription
Clinical staging at baseline:
- Stage 2 Hypertension
- Hypertensive Crisis

### 4. BP Level After Medication
Post-treatment BP classification used for transition and outcome analysis:
- Normal
- Elevated
- Isolated Diastolic Hypertension
- Stage 1 Hypertension
- Stage 2 Hypertension
- Hypertensive Crisis

---


---

## Results Summary

### Medication Adherence

| Adherence Level | Patients | % of Total | Control Rate |
|---|---|---|---|
| Good | 105 | 30% | **15.2%** |
| Moderate | 132 | 38% | 11.4% |
| Poor | 113 | 32% | **1.8%** |

The 8× control gap between good and poor adherers makes adherence the most actionable single predictor — identifiable before treatment begins.

### BP Stage Transition (Before → After Medication)

| Baseline Stage | n | Normal | Elevated | Isolated Diastolic | Stage 1 | Stage 2 | Crisis |
|---|---|---|---|---|---|---|---|
| Stage 2 Hypertension | 265 | 7 | 29 | 6 | 40 | 183 | 0 |
| Hypertensive Crisis | 85 | 0 | 0 | 0 | 0 | 74 | 11 |

Hypertensive Crisis patients did not reach controlled status under any drug class in this cohort.

### Control Rate by Age Group

| Age Group | Control Rate |
|---|---|
| Under 45 | 8.9% |
| 46–55 | **12.3%** |
| 56–65 | 10.2% |
| 66+ | 8.0% |

### Notable Observation — ACE Inhibitor Paradox
ACE Inhibitor produced the **second-highest average systolic BP reduction** in the dataset (~15.9 mmHg), yet recorded **0% control** across all 45 patients. This suggests the drug is being prescribed to patients with very high baseline BP who respond partially but cannot reach the controlled threshold from their starting point — a potential patient selection issue warranting further investigation.

### Zero-Comorbidity Open Question
Patients with no documented comorbidity still present with hypertension and achieved a **99.8% failure rate** at 3 months. This is clinically paradoxical and suggests undocumented secondary aetiology. These patients should receive structured secondary investigation rather than pharmacological escalation alone.

---

## Recommendations

### 1. Prioritize Adherence-Focused Interventions
- Implement patient education programs before and during treatment
- Introduce reminders, follow-up calls, or digital adherence tools
- Simplify medication regimens where clinically appropriate

### 2. Intensify Treatment for High-Risk Patients Early
For patients presenting with SBP ≥160 mmHg and/or multiple comorbidities:
- Consider early combination therapy as first-line
- Implement closer clinical monitoring schedules
- Apply more aggressive BP management targets

### 3. Optimise Drug Selection by Comorbidity Profile
- **Diabetes Mellitus patients** → prefer ARB (RAAS-protective)
- **CKD patients** → re-evaluate ACE Inhibitor use; monitor eGFR closely
- **Obesity patients** → anticipate metabolic treatment resistance; consider combination therapy
- **Hypertensive Crisis patients** → require intensive management beyond standard outpatient prescribing

### 4. Focus on Quality of Clinical Visits
Visit frequency showed modest effect in isolation. The clinical emphasis should shift to what happens *during* the visit:
- Medication counselling and side effect discussion
- Lifestyle modification guidance (salt intake, physical activity, weight management)
- Adherence assessment and reinforcement at every contact point

---

## Glossary

| Term | Definition |
|---|---|
| **Diabetes Mellitus** | A chronic metabolic disorder characterised by hyperglycaemia due to insulin deficiency or resistance |
| **CKD (Chronic Kidney Disease)** | Long-term loss of kidney function (>3 months), measured by eGFR <60 ml/min/1.73m² or elevated urine albumin |
| **Dyslipidemia** | An unhealthy imbalance of blood lipids — elevated LDL/triglycerides and/or reduced HDL cholesterol |
| **Obesity** | A chronic disease defined by excessive body fat accumulation posing health risks |
| **Comorbidity** | The coexistence of two or more chronic conditions in the same patient |
| **Control Rate** | The percentage of patients who successfully reached their clinical BP target |
| **RAAS** | Renin-Angiotensin-Aldosterone System — a hormone system regulating blood pressure and fluid balance |
| **eGFR** | Estimated Glomerular Filtration Rate — a measure of kidney filtering capacity |
| **ARB** | Angiotensin Receptor Blocker — a class of antihypertensive medication |
| **ACE Inhibitor** | Angiotensin-Converting Enzyme Inhibitor — another antihypertensive drug class |

---

## Author

**Ayomide Olayiwola**

*Hypertension Cardiology Centre Analytics Report — 2024 Cohort*

---

> **Note:** This analysis is based on observational patient records. All findings are descriptive and correlational. Clinical decisions should incorporate broader patient context and professional medical judgement.
