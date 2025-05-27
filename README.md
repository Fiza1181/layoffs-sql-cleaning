# 🧹 layoffs-sql-cleaning

SQL project for cleaning a layoffs dataset using MySQL. This project focuses on identifying and fixing data quality issues like duplicates, inconsistent formatting, null values, and incorrect data types.

---

## 📂 Project Structure

layoffs-sql-cleaning
layoffs_data_cleaning.sql # Main SQL script with all cleaning steps
layoffs_raw.csv # Raw dataset


---

## 📋 Project Description

This project demonstrates how to clean real-world data using SQL. The dataset contains global tech layoffs data, and the cleaning process includes:

- Removing duplicate records using CTEs and `ROW_NUMBER()`
- Trimming whitespace and fixing inconsistent text entries (e.g., industry names)
- Converting date strings to proper `DATE` format
- Handling `NULL` and empty values in key columns
- Standardizing country and company names
- Dropping unnecessary rows and columns

---

## 🔧 Tools Used

- **MySQL**
- **SQL Window Functions**
- **Common Table Expressions (CTEs)**

---

## 📊 Dataset

- 📁 File: `data/layoffs_raw.csv`
- 📌 Source: [Add the original dataset source link here, e.g., Kaggle]

---

## 🚀 How to Use

1. Import the raw CSV file into your MySQL database (if available).
2. Run the `layoffs_data_cleaning.sql` script step-by-step.
3. Verify results using `SELECT` queries after each cleaning phase.
4. Modify or extend the script to suit other datasets or business needs.

---

## 🧠 Key SQL Concepts Used

- `ROW_NUMBER()` for identifying duplicates
- `CTE (Common Table Expression)` for temporary views
- `TRIM()` and `LIKE` for standardizing text fields
- `STR_TO_DATE()` for formatting date fields
- `DELETE`, `UPDATE`, and `ALTER` statements

---

## 📌 Example Query Snippet

```sql
-- Remove duplicates using a CTE and ROW_NUMBER()
WITH duplicate_cte AS (
  SELECT *,
         ROW_NUMBER() OVER (
           PARTITION BY company, location, industry, total_laid_off, percentage_laid_off, date, stage, country
           ORDER BY date DESC
         ) AS row_num
  FROM layoffs_staging2
)
DELETE FROM layoffs_staging2
WHERE row_num > 1;


