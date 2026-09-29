# Customer Data Cleaning & Preprocessing

A robust data preprocessing pipeline designed to sanitize raw customer records, handle anomalies, and optimize memory usage 

---

## 🔍 Data Quality Issues & Remediation Strategy 

cleaning a dataset of the information of customers

preprocessing 


### 1. Duplicate Records
* **Issue:** Redundant customer rows leading to skewed distributions and bias.
* **Fix:** Identified via boolean masking and removed using `df.drop_duplicates()`

### 2. Missing Value Imputation
* **Issue:** Missing entries detected in critical numerical features: `age` and `total_spending`.
* **Fix:** Dropped "age" and fill "tota_spending"

### 3. Schema & Memory Optimization (Type Casting)
* **Issue:** Default `float64` datatypes consumed excessive memory and inappropriately represented discrete counts (like age).
* **Fix:** 
  * Downcasted numerical features (e.g., converted `age` to pandas nullable integer `Int16`).
  * Optimized entire schema data types, significantly reducing overall DataFrame memory footprint.

### 4. Date & Temporal Normalization
* **Issue:** `signup_date` was stored as a raw string/object type.
* **Fix:** Parsed into standardized ISO-8601 timestamps using `pd.to_datetime(df['signup_date'])` to enable temporal feature engineering.


### 5. Invalid / Domain-Logic Violations
* **Issue:** Unrealistic human records identified (e.g., `age == 145`).
* **Fix:** Filtered out logically impossible values based on domain-level validation rules (`age < 100`).

### 6. Outlier Detection
* **Issue:** Extreme anomalies in numerical features (e.g., `total_spending`).
* **Fix:** Visualized feature distributions via Boxplots and handled extreme leverage points using IQR (Interquartile Range) filtering.


## 📊 Summary of Optimization

| Metric / Stage | Raw Dataset    | Cleaned Dataset |
| :--- |:---------------| :--- |
| **Total Rows** | 61             | 56 |
| **Missing Values** | 2              | 0 |
| **Memory Footprint** | 8.2+ KB | 6.6+ KB |
