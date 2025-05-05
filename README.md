# food

# Introduction

# The ETL process focuses on preprocessing a dataset capturing food choices, eating habits, and preferences among 126 college students from Mercyhurst University (sourced from Kaggle). 

# Dataset

# The source dataset (`food_coded.csv`) contains 61 attributes covering demographics (GPA, gender), nutrition knowledge, eating habits (comfort food, cooking frequency, eating out), dietary preferences, and open-ended responses about ideal diets and healthy meals. The raw # data includes missing values, inconsistent formatting, and mixed data types, necessitating thorough preprocessing.

# ETL Pipeline and Preprocessing Steps

# An ETL (Extract, Transform, Load) pipeline was implemented using Python and pandas to clean and prepare the data.

# 1.  **Extract:** Reads the raw `food_coded.csv` file.
# 2.  **Transform:** Applies a series of cleaning and standardization functions:
#    * `clean_column_names`: Formats column names (lowercase, underscores).
#    * `drop_duplicated_column`: Removes the original `comfort_food_reasons_coded` column and renames its duplicate counterpart.
#    * `clean_float_columns`: Extracts numeric values from `gpa` and `weight` columns (handling text like "lbs") and converts them to float.
#    * `handle_missing_values`: Imputes missing values using various strategies: inferred fixed values (`calories_day`, `calories_scone`, `employment`), median (`gpa`, `weight`), mode (most other coded columns), and "not specified" (open-ended text columns).
#    * `clean_open_ended_columns`: Cleans text data in open-ended columns (lowercase, removes punctuation/special characters, normalizes whitespace). *Note: Lemmatization/stop word removal is included but currently commented out in the code.* Drops rows where open-ended text becomes empty after cleaning.
#    * `remove_outliers`: Removes outlier values from `gpa` (values outside Q1-1.5*IQR to 4.0) and `weight` (values outside Q1-1.5*IQR to Q3+1.5*IQR) using the IQR method.
#    * `standardize_float_columns`: Scales `gpa` (Max Scaling by 4.0) and `weight` (Min-Max Scaling) to a 0-1 range.
#    * `standardized_cuisine`: Standardizes the `fav_cuisine` column by extracting predefined keywords (e.g., 'italian', 'mexican'), handling multiple mentions (e.g., 'italian-thai'), mapping negative/no preference entries to 'unspecified', and defaulting non-matches to 'other'.
# 3.  **Load:** Saves the processed DataFrame to `processed_food_coded.csv`.
