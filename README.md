# Medicaid Billing Anomaly Detection (Forensic Analysis)

## Overview
This project analyzes Medicaid behavioral health billing data to identify statistically abnormal and operationally infeasible billing patterns.

The goal is to distinguish normal variation from high-risk anomalies by combining statistical methods with real-world operational constraints.

**Built as a Python-based analysis pipeline to model billing baselines and detect anomalies.**

---

## Key Insight
While reimbursement rates declined by 16.6%, a subset of providers showed a 22% increase in billed service volume, indicating a divergence from expected economic behavior.

---

## Methodology

### 1. Baseline Modeling
- Calculated median billing per beneficiary by HCPCS code (H2019) at the regional level  
- Defined normal ranges using statistical thresholds (Z-score, % above median)

### 2. Outlier Detection
- Flagged providers with:
  - >3x regional median billing  
  - Z-score > 3  

### 3. Constraint-Based Analysis
Applied real-world feasibility rules:

- **Temporal Constraint:** Maximum daily service capacity set at 14 billable hours  
- **Geographic Constraint:** Same-day services across distant locations evaluated against minimum travel time  
- **Combined Constraint:** Total required service time + travel time must remain within realistic operational limits  

---

## Case Study (Representative Example)

**Anomaly Type:** Temporal + Geographic Constraint Violation  

- Same-day billing recorded across distant locations  
- ~5+ hours of service time recorded  
- ~6 hours required travel between locations  
- Additional same-day claims increase total required time  

**Conclusion:**  
When combining service time, travel requirements, and additional same-day billing activity, total required time exceeds realistic daily operational capacity and implies overlapping service windows.

---

## Example Output

| Provider | Billing per Beneficiary | Regional Median | % Above Median | Z-Score | Flag |
|----------|------------------------|-----------------|----------------|--------|------|
| Provider A | $4,200 | $1,100 | 281% | 4.2 | Temporal/Geographic Constraint Violation |
| Provider B | $3,850 | $1,100 | 250% | 3.8 | Billing Divergence |
| Provider C | $5,100 | $1,100 | 363% | 5.1 | Extreme Volume Outlier |

---

## Key Takeaways
- Combining statistical methods with real-world constraints improves anomaly detection reliability  
- Pure statistical outliers are not sufficient without feasibility validation  
- Constraint violations provide stronger signals for further investigation  

---

## Limitations
- Medicaid data may include lagged or adjusted claims  
- Some edge cases (e.g., shared providers or telehealth scenarios) may require additional validation  
- This analysis does not include full claim-level audit verification  

---

## Repo Contents
- `analysis.py` – core anomaly detection logic  
- `sample_data.csv` – example dataset  
- `README.md` – summary and findings  

---

## Disclaimer
This project is for educational and analytical purposes only.  
All provider data has been anonymized.  
This analysis does not constitute a formal investigation or allegation of fraud.
