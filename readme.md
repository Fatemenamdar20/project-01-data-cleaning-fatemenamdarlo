# Customer Data Cleaning

Cleaning and validating a small customer dataset (61 rows, 17 columns) with pandas: duplicates, missing values, data types, impossible values, and inconsistent records.

## Dataset

`First_Dataset.xlsx` contains one row per customer.

| Column | Description |
|---|---|
| `customer_id` | Unique customer identifier |
| `first_name`, `gender`, `age` | Customer demographics |
| `city`, `province` | Customer location |
| `signup_date` | Date the customer signed up |
| `membership_tier` | Bronze / Silver / Gold / VIP |
| `purchase_count` | Number of purchases |
| `avg_order_value` | Average value of one order |
| `total_spending` | Total amount spent |
| `last_purchase_days` | Days since the last purchase |
| `payment_method`, `device` | How the customer pays / which device they use |
| `discount_used` | Whether the customer used a discount (Yes/No) |
| `returned_items` | Number of returned items |
| `satisfaction_score` | Satisfaction rating from 1 to 5 |

> [the data is synthetic.]

## Data Quality Issues and How They Were Handled

| # | Issue | Action                                                                   | Rows affected |
|---|---|--------------------------------------------------------------------------|---|
| 1 | Exact duplicate row (customer 1014) | Removed with `drop_duplicates()`                                         | 1 |
| 2 | Missing `age` | [Dropped the row]                                                        | 1 |
| 3 | Missing `total_spending` | [Recomputed as `purchase_count × avg_order_value`]                       | [0 removed] |
| 4 | Impossible age (145) | Replaced; with median[45]                                                | 1 |
| 5 | Customer with `purchase_count = 0` | [Removed: no purchases, so not an active customer]                       | 1 |
| 6 | `total_spending` inconsistent with `purchase_count × avg_order_value` (e.g. customer 1030: 25,000 vs about 4,079) | Corrected                                                              | [n] |
| 7 | Wrong data types | `age` and count columns cast to nullable integers, `signup_date` parsed to datetime | all |

**Result:** 61 rows in, 58 rows out, 0 missing values.

Large spenders (over 10,000) whose totals are consistent with their order data were **kept**, since they are real customers and not errors.

## Limitations

- The dataset is small (about 57 clean rows), so group differences may be due to chance.
- `discount_used` is recorded per customer, not per purchase, so the effect of a discount on a specific order cannot be measured.
- [Any remaining inconsistencies you did not resolve.]

## How to Run

```bash
git clone https://github.com/Fatemenamdar20/project-01-data-cleaning-fatemenamdarlo.git
cd project-01-data-cleaning-fatemenamdarlo
pip install -r requirements.txt
jupyter notebook data_cleaning.ipynb
```

## Project Structure

```
.
├── data_cleaning.ipynb    # cleaning and exploration
├── First_Dataset.xlsx     # raw data
├── requirements.txt
└── README.md
```

## Tools

Python, pandas, matplotlib, openpyxl