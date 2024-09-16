# Data Quality Validation for Data Warehousing

## Overview

This project focuses on conducting comprehensive data quality checks within a data warehousing environment. It demonstrates the use of a Python-based framework integrated with PostgreSQL to validate data integrity, ensuring accuracy and consistency. The key objective is to automate checks for null values, duplicates, min/max ranges, and invalid records, providing a scalable approach for maintaining data quality.

## Key Features

- **Null Value Check:** Identifies and reports null values in the dataset.
- **Duplicate Value Check:** Detects duplicate entries to ensure data uniqueness.
- **Min-Max Range Check:** Validates numerical ranges to ensure values fall within the correct range.
- **Invalid Value Check:** Identifies invalid entries based on predefined valid values.
- **Data Quality Report Generation:** Generates reports based on the test results.

## Project Structure

- **`dataqualitychecks.py`**: Contains the core functions for validating data (e.g., null values, duplicates, min-max ranges, valid values).
- **`dbconnect.py`**: Handles connection to the PostgreSQL database.
- **`mytests.py`**: Contains custom data quality tests applied to specific tables and columns.
- **`generate-data-quality-report.py`**: Generates a report summarizing the data quality checks.
- **`setupstagingarea.sh`**: Sets up the staging area by creating the database, schema, and loading the data into the PostgreSQL database.

## Example Tests

### 1. Check for Null Values
```python
test1 = {
    "testname": "Check for nulls",
    "test": check_for_nulls,
    "column": "year",
    "table": "DimMonth"
}
```

### 2. Check for Min-Max Range
```python
test2 = {
    "testname": "Check for min and max",
    "test": check_for_min_max,
    "column": "quarter",
    "table": "DimMonth",
    "minimum": 1,
    "maximum": 4
}
```

### 3. Check for Valid Values
```python
test3 = {
    "testname": "Check for valid values",
    "test": check_for_valid_values,
    "column": "quartername",
    "table": "DimMonth",
    "valid_values": {'Q1', 'Q2', 'Q3', 'Q4'}
}
```

### 4. Check for Diplicates
```python
test4 = {
    "testname": "Check for duplicates",
    "test": check_for_duplicates,
    "column": "customerid",
    "table": "DimCustomer"
}
```

## Setup and Execution

### Prerequisites
* Python 3.x
* PostgreSQL
* psycopg2 (Python library for PostgreSQL)

### Step 1: Download the files
Clone the repo
```bash
git clone https://github.com/VM-137/billing-data-warehouse-quality-check.git
```

### Step 2: Database Connection
Update the dbconnect.py file to configure the PostgreSQL connection:
```python
def connect():
    conn = psycopg2.connect(
        host="your_host",
        database="your_db",
        user="your_username",
        password="your_password"
    )
    return conn
```

### Step 3: Add Custom Tests
Add your custom data quality tests in the mytests.py file. Each test should follow the structure below:
```python
test = {
    "testname": "Your test description",
    "test": test_function,
    "column": "column_name",
    "table": "table_name"
}
```

### Step 3: Running the Tests
Run the tests and generate the report by executing the following command:
```bash
python3 generate-data-quality-report.py
```

## Results and Reporting
After running the tests, the generate-data-quality-report.py script generates a report summarizing the outcomes of the tests. The report will include:

* Number of null values detected
* Duplicate records found
* Entries that are outside the min-max range
* Invalid values present in the dataset

## Future Improvements

* Automated Scheduling: Use tools like Airflow or Cron to schedule and run the data quality tests automatically.
* Test Expansion: Add more custom data quality checks to improve validation coverage.
* Real-Time Monitoring: Set up real-time alerts for data quality issues to enable faster response and resolution.