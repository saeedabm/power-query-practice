# Customer Orders — Power Query Data Cleaning

Practice project: cleaning and transforming a messy customer orders dataset using Power Query in Power BI.

## The Problem

The raw dataset came in with several common real-world issues:

| Issue | Example |
|---|---|
| Multiple products in one cell | `"A,B,C"` instead of separate rows |
| Inconsistent date formats | `15-01-2024`, `2024/01/18`, `20-Jan-2024` |
| Currency stored as text | `"₹1,20,000"` instead of a number |
| Inconsistent text casing | `Delivered` / `DELIVERED` / `delivered` |
| Leading/trailing spaces | `"  Arun Das  "` |
| Blank values | Missing region, missing order amount |

## What I Did

Using Power Query, I:

1. **Unpivoted** the `products_purchased` column so each product a customer bought has its own row
2. **Standardized dates** to a single consistent format
3. **Cleaned currency values** — removed `₹` symbol and commas, converted to a proper number type
4. **Standardized text casing** on `status` and `customer_name` using Capitalize Each Word
5. **Trimmed extra spaces** from customer names
6. **Handled blanks intentionally**:
   - Blank `region` → labeled `"Unknown"` (so the row is still counted in groupings)
   - Blank `amount` → flagged with a conditional column (`"Missing Amount"`) instead of guessing a value
7. **Reviewed the output** and caught one record where a name hadn't been capitalized correctly on the first pass — fixed and re-validated

## Before → After

**Before:** one row per order, products jammed into a single comma-separated cell, 4 different date formats, currency as text, inconsistent casing.

**After:** one row per product per order, clean consistent dates, numeric currency, standardized casing, and explicit handling of missing data instead of silent gaps.

## Key Takeaway

Raw data rarely comes ready to analyze. A blank cell isn't always the same problem — a missing measure (like amount) should be flagged for review rather than filled with a guess, while a missing dimension (like region) is safer to label clearly so the row isn't lost from your analysis. Getting this distinction right is most of the real work before any dashboard or chart happens.

## Files

- `raw_customer_orders.xlsx` — original messy data
- `cleaned_customer_orders.xlsx` — transformed output after Power Query steps

## Tools

Power BI · Power Query (M)
