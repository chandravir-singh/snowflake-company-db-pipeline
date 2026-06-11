# 🏢 Snowflake Company Data Pipeline (Stage + Pipe + Stream + Task + Merge) 🚀

---

## 📌 Project Overview

This project demonstrates a **real-time data pipeline in Snowflake** using:

- ✅ External Stage (Data Loading)
- ✅ Snowpipe (Continuous Ingestion)
- ✅ Streams (Change Data Capture - CDC)
- ✅ Tasks (Automation)
- ✅ MERGE (Upsert Logic)
- ✅ Aggregation (Department Summary)

The pipeline processes employee data and maintains **department-level summary metrics**.

---

## 🏗 System Architecture

```

```
       ┌───────────────┐
       │  CSV FILES    │
       └──────┬────────┘
              ↓
       ┌───────────────┐
       │   STAGE       │ (@emp_stage)
       └──────┬────────┘
              ↓
       ┌───────────────┐
       │   PIPE        │ (Snowpipe)
       └──────┬────────┘
              ↓
       ┌───────────────┐
       │  EMP_RAW      │ (Raw Table)
       └──────┬────────┘
              ↓
       ┌───────────────┐
       │  STREAM       │ (CDC)
       └──────┬────────┘
              ↓
       ┌───────────────┐
       │  TASK         │ (Automation)
       └──────┬────────┘
              ↓
       ┌───────────────┐
       │ EMP_SUMMARY   │ (Final Table)
       └───────────────┘
```

```

---

## 📂 Project Structure

```

company-data-pipeline/
│
├── COMPANY\_DB.SQL ✅ Main pipeline script
└── README.md ✅ Documentation

````

---

## 🛠 Technologies Used

- Snowflake SQL
- Snowpipe (Auto Ingestion)
- Streams (CDC)
- Tasks (Automation)
- MERGE (Upsert Logic)

---

## ✅ Step-by-Step Workflow

---

### 🔹 STEP 1: Create Database

```sql
CREATE DATABASE COMPANY_DB;
````

👉 Creates a dedicated database for the pipeline.

***

### 🔹 STEP 2: Create Raw Table

```sql
CREATE TABLE EMP_RAW
```

👉 Stores **raw employee data**.

Columns:

* EMP\_ID
* NAME
* DEPARTMENT
* SALARY

***

### 🔹 STEP 3: Create Stage

```sql
CREATE STAGE emp_stage;
```

👉 Used to upload CSV files.

***

### 🔹 STEP 4: Load Data (Bulk Load)

```sql
COPY INTO EMP_RAW
FROM @emp_stage
FILE_FORMAT = (TYPE = 'CSV' SKIP_HEADER = 1);
```

👉 Loads initial data from stage.

***

## 🔥 Snowpipe (Continuous Data Ingestion)

### 🔹 STEP 5: Create Pipe

```sql
CREATE PIPE emp_pipe
```

👉 Automatically loads new files from stage.

***

### 🔹 Refresh Pipe

```sql
ALTER PIPE emp_pipe REFRESH;
```

👉 Triggers loading of existing files.

***

## ✅ STEP 6: Create Stream (CDC)

```sql
CREATE STREAM emp_stream ON TABLE EMP_RAW;
```

👉 Tracks:

* ✅ New records
* ✅ Updates
* ✅ Deletes

***

## ✅ STEP 7: Create Summary Table

```sql
CREATE TABLE EMP_SUMMARY
```

👉 Stores:

* Total employees per department
* Total salary per department

***

## ✅ STEP 8: Task Automation + MERGE 🔥

```sql
CREATE TASK emp_task
```

### ✅ What it does:

* Reads incremental data from stream
* Aggregates by department
* Updates summary table

***

## 🔥 MERGE LOGIC (CORE)

### ✅ WHEN MATCHED

```sql
UPDATE
```

👉 Adds new values to existing department

***

### ✅ WHEN NOT MATCHED

```sql
INSERT
```

👉 Creates new department record

***

## ✅ DATA FLOW LOGIC

| Step     | Action               |
| -------- | -------------------- |
| New data | Loaded into EMP\_RAW |
| Stream   | Captures change      |
| Task     | Runs every 1 minute  |
| Merge    | Updates summary      |

***

## ✅ STEP 9: Start Task

```sql
ALTER TASK emp_task RESUME;
```

***

## ✅ STEP 10: Test Pipeline

```sql
INSERT INTO EMP_RAW VALUES (101, 'Test', 'IT', 50000);
```

👉 Simulates incoming data

***

## ✅ STEP 11: Verify Output

```sql
SELECT * FROM EMP_SUMMARY;
```

***

## 📊 Example Output

```
DEPARTMENT | TOTAL_EMP | TOTAL_SALARY
--------------------------------------
IT         | 3         | 150000
HR         | 2         | 90000
```

***

## 🧠 Key Concepts Learned

This project demonstrates:

* ✅ Real-time data ingestion using Snowpipe
* ✅ Incremental processing using Streams
* ✅ Automation using Tasks
* ✅ Upsert logic using MERGE
* ✅ Aggregation pipeline design

***

## ⚠ Important Notes

### ✅ Task must be active

```sql
ALTER TASK emp_task RESUME;
```

***

### ✅ Warehouse must be running

```sql
ALTER WAREHOUSE COMPUTE_WH RESUME;
```

***

### ✅ Stream is consumed once

👉 Data disappears after task processes it

***

## 🚀 Real-World Use Cases

* Department-wise reporting dashboards
* HR Analytics
* Real-time aggregation pipelines
* Enterprise Data Warehouse

***

## 🚀 Future Enhancements

* Enable AUTO\_INGEST = TRUE (real-time Snowpipe)
* Add S3 integration
* Add error handling
* Build Power BI dashboard

***

## 👨‍💻 Author

**Chandravir Singh**  
Software Engineer | Data Engineer

***

## ⭐ If You Like This Project

Give it a ⭐ on GitHub and share 🚀

```

---

# ✅ ✅ What You Should Do Now

1. Create file:
```

README.md

````

2. Paste above content

3. Run:

```bash
git add COMPANY_DB.SQL README.md
git commit -m "Added Company Data Pipeline with Snowpipe, Streams, Tasks"
git push
````

***

# 🎯 FINAL RESULT

```
company-data-pipeline/
│
├── COMPANY_DB.SQL ✅
└── README.md ✅ (Professional)
```

***
