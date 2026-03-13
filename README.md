🛠️ Data Cleaning in SQL: World Layoffs Dataset
📌 Project Overview
The objective of this project is to clean and standardize the World Layoffs dataset to make it ready for exploratory analysis. Using MySQL, I transformed raw, messy data into a structured format by applying advanced SQL techniques such as CTEs, Window Functions, and Self-Joins.

📁 Dataset Source
The raw data used in this project can be found here: https://github.com/KanakSharma0308/SQL-Data-Cleaning/blob/main/layoffs.xlsx

🛠️ Skills & Tools Used
Database: MySQL Workbench
SQL Concepts: Data Standardization, Null Value Handling, Schema Modification
Advanced Techniques: Common Table Expressions (CTEs), Window Functions (ROW_NUMBER())

🚀 Data Cleaning Steps
Following a structured data engineering workflow, I performed the following steps:

1. Staging the Data
To protect the integrity of the original dataset, I created a staging table. This ensures that all cleaning operations are performed on a copy, leaving the raw data untouched.
SQL
CREATE TABLE layoff_staging LIKE layoffs;
INSERT layoff_staging SELECT * FROM layoffs;

2. Removing Duplicates
I identified duplicate records by using the ROW_NUMBER() window function partitioned across all primary columns (Company, Location, Industry, Date, etc.).
Logic: Any record with a row_num greater than 1 was flagged as a duplicate and removed.
Why: This ensures each layoff event is only counted once in future analysis.

3. Standardizing Data
Raw data often has inconsistencies. I performed the following transformations:
Industry Names: Grouped variations like 'Crypto Currency' and 'CryptoCurrency' into a single standard 'Crypto' category.
Country Names: Cleaned trailing characters and punctuation from country entries (e.g., fixing "United States.").
Date Formatting: Converted the date column from a text string to a proper DATE format using STR_TO_DATE for time-series analysis.

4. Handling Nulls and Missing Values
Self-Joins: For companies with missing industry data, I performed a self-join to populate the nulls using existing data from other rows belonging to the same company.
Data Pruning: Removed rows where both total_laid_off and percentage_laid_off were null, as these records did not provide actionable insights for analysis.

📊 Final Result
The dataset is now standardized, unique, and formatted correctly. The total record count has been optimized, and it is now ready for the Exploratory Data Analysis (EDA) phase.
