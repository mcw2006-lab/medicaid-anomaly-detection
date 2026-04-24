# Medicaid Billing Anomaly Detection (Forensic Analysis)

## Overview
This project analyzes Medicaid behavioral health billing data to identify statistically abnormal and operationally infeasible billing patterns.

The goal is to distinguish normal variation from high-risk anomalies using both statistical methods and real-world constraints.

---

## Key Insight
While reimbursement rates declined by 16.6%, a subset of providers showed a 22% increase in billing volume, indicating a divergence from expected economic behavior.

---

## Methodology

### 1. Baseline Modeling
- Calculated median billing per beneficiary by HCPCS code and region
- Defined normal ranges using statistical thresholds

### 2. Outlier Detection
- Flagged providers with:
  - >3x regional median billing
  - Z-score > 3

### 3. Constraint-Based Analysis
Applied real-world feasibility rules:
- Maximum daily service capacity (14 hours)
- Geographic consistency (travel time constraints)

---

## Case Study (Simplified Example)

**Anomaly Type:** Temporal + Geographic Constraint Violation  

- Same-day billing recorded across distant locations  
- ~5+ hours of service + ~6 hours travel time  
- Additional same-day claims push total required time beyond realistic operational limits  

**Conclusion:**  
Indicates high-probability anomaly due to overlapping service constraints.

---

## Example Output

| Provider | Billing per Beneficiary | Regional Median | % Above Median | Z-Score | Flag |
|----------|------------------------|-----------------|----------------|--------|------|
| Provider A | $4,200 | $1,100 | 281% | 4.2 | Constraint Violation |
| Provider B | $3,850 | $1,100 | 250% | 3.8 | Billing Divergence |
| Provider C | $5,100 | $1,100 | 363% | 5.1 | Extreme Outlier |

---

## Key Takeaways
- Combining statistical methods with real-world constraints improves anomaly detection
- Pure statistical outliers are not always sufficient without feasibility checks
- Constraint violations provide stronger signals for investigation

---

## Limitations
- Data may include lagged or adjusted claims
- Some edge cases (e.g., shared providers, telehealth) may require deeper validation

---

## Disclaimer
This project is for educational and analytical purposes only.  
All provider data has been anonymized.  
This analysis does not constitute a formal investigation or allegation.
