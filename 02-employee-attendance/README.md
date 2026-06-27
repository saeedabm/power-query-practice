# Employee Attendance — Power Query Data Transformation

Practice project: transforming a monthly attendance report from a wide, human-readable format into a clean, analysis-ready table using Power Query.

## The Problem

The raw data had months spread across separate columns — a very common format in exported HR/payroll reports, built for reading, not analysis.

| Issue | Example |
|---|---|
| Months as columns | `Jan_2024`, `Feb_2024`, `Mar_2024`... instead of a single Month column |
| Inconsistent missing values | Some months blank, others showed the text `"N/A"` |
| Days Present typed as text | Numbers stored as text, not usable in calculations |
| No working days reference | Raw data had no way to calculate attendance % directly |

## What I Did

1. **Unpivoted** the month columns (`Jan_2024` → `Jun_2024`) into two columns: `Month` and `Days Present`
2. **Standardized missing values** — converted the text `"N/A"` to true nulls so it matched the blank cells
3. **Filtered out null attendance rows** using the column filter, instead of a blanket "Remove Blank Rows" (which would have caught more than intended)
4. **Fixed the Days Present column type** — it was still typed as Text after unpivoting, so a quick `ABC → 123` data type fix was required before any calculation would work
5. **Built a separate Working_Days reference table** (Month → Working Days), since the raw data had no column for this
6. **Merged** the reference table into the attendance data on `Month` (Left Outer join)
7. **Added a calculated column** — `Attendance_% = Days Present / Working_Days * 100`, rounded to 1 decimal

## Before → After

**Before:** one row per employee, six separate month columns, mixed null representations, text-typed numbers, no way to calculate attendance rate.

**After:** one row per employee per month, clean `Month` and `Days Present` columns, a merged `Working_Days` reference, and a calculated `Attendance_%` ready for visualization.

## Key Takeaway

Real datasets often don't contain every column needed for the metric you're asked to calculate. Working_Days didn't exist anywhere in the raw export — it had to be built as a separate reference table and merged in. Recognizing a missing input before it breaks your formula is as much a part of the job as the transformation steps themselves.

Also: a column that *displays* as numbers isn't necessarily *typed* as numbers. Always confirm the data type icon, not just how the values look.

## Files

- `raw_employee_attendance.xlsx` — original wide-format data
- `working_days_reference.xlsx` — supporting reference table (Month → Working Days)
- `transformed_employee_attendance.xlsx` — final transformed output with Attendance %

## Tools

Power BI · Power Query 
