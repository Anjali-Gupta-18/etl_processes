ETL Data Loading into SQL Server

Overview

This project demonstrates how to load transformed data into a SQL Server database using Python and the `pyodbc` library. It includes a function to insert Netflix title data into a SQL Server table. The script uses Windows Authentication for establishing a secure connection to the database.

Prerequisites

Before running this script, ensure you have the following:

1. Python Environment:
   - Install Python (version 3.6 or higher recommended).
   - Required libraries:
     - `pandas`
     - `pyodbc`
     - Install these libraries using the following command:
       ```bash
       pip install pandas pyodbc
       ```

2. SQL Server:
   - A running instance of SQL Server (e.g., `SQLEXPRESS`).
   - A database named `etl_demo`.

3. Data:
   - A properly transformed dataset (e.g., a Pandas DataFrame named `transformed_data`) containing Netflix titles with the following columns:
     - `show_id`
     - `type`
     - `title`
     - `director`
     - `cast`
     - `country`
     - `date_added`
     - `release_year`
     - `rating`
     - `duration`
     - `listed_in`
     - `description`


Script Details

Functions

1. `load_data_sql_server`:
   - This function connects to a SQL Server database and inserts rows from a Pandas DataFrame into a table named `netflix_titles`.

2. `create_table_sql_server` (Assumed to exist):
   - Presumably, this function creates the `netflix_titles` table in the SQL Server database with appropriate schema.

Parameters

- `server_name`:
  - Replace `'LAPTOP-Instanceid\SQLEXPRESS'` with your SQL Server instance name.
- `database_name`:
  - Name of the target database (`etl_demo` by default).
- `data`:
  - A Pandas DataFrame containing the transformed Netflix data.

Table Schema

The `netflix_titles` table should have the following schema:

```sql
CREATE TABLE netflix_titles (
    show_id NVARCHAR(50) PRIMARY KEY,
    type NVARCHAR(50),
    title NVARCHAR(255),
    director NVARCHAR(255),
    cast NVARCHAR(MAX),
    country NVARCHAR(255),
    date_added DATE,
    release_year INT,
    rating NVARCHAR(50),
    duration NVARCHAR(50),
    listed_in NVARCHAR(MAX),
    description NVARCHAR(MAX)
);
```


How to Run the Script

1. Setup the Database:
   - Ensure the `etl_demo` database exists.
   - Execute the table creation query (if not already done).

2. Run the Script:
   - Replace the `server_name` and `database_name` variables with your specific details.
   - Ensure the `transformed_data` DataFrame is loaded and ready.
   - Run the Python script to load the data.

3. Verify the Data:
   - Query the `netflix_titles` table to ensure the data has been loaded:
     ```sql
     SELECT * FROM netflix_titles;
     ```

If an error occurs during the data loading process, it will be printed in the console with the exact issue for debugging. Common errors include:

- Duplicate primary keys (`Violation of PRIMARY KEY constraint`).
- Incorrect server or database names.
- Data type mismatches.

Example Output

Upon successful execution, you should see:
```
Data loaded successfully into SQL Server!
```

If an error occurs, you will see:
```
Error loading data: <Error details>
```
You can remove this error by running the query "delete from table" in the database then again try to run the Python script to load it to the database
