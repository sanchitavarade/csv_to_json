

# 📊 CSV → JSON API (Node.js + PostgreSQL)

## Overview

A simple Express API that uploads CSV files, parses them into nested JSON, and stores records in PostgreSQL. It streams data efficiently and returns an age-group distribution summary.

---

## ✨ Features

* Custom CSV parser (handles quotes & dotted headers)
* Streams large files line-by-line
* Batch inserts into Postgres (`BATCH_SIZE` configurable)
* Returns age distribution: `<20`, `20–40`, `40–60`, `>60`

---

## ⚙️ Setup

```bash
git clone <repo-url>
cd csv-to-json-api
npm install
cp .env.example .env
```

Edit `.env` with your DB credentials:

```
PG_HOST=localhost
PG_USER=postgres
PG_PASSWORD=your_password
PG_DATABASE=your_database
BATCH_SIZE=1000
```

Create the table:

```bash
psql -h $PGHOST -U $PGUSER -d $PGDATABASE -f upload.sql
```

---

## 🚀 Run

```bash
npm start
```

Upload a CSV:

```bash
curl -X POST -F "file=@sample_data/sample.csv" http://localhost:3000/upload
```

**Response:**

```json
{
  "total_records": 200,
  "age_distribution": { "<20": 10, "20-40": 70, "40-60": 15, ">60": 5 }
}
```

---

## 🧠 Tech Stack

* Node.js + Express
* PostgreSQL
* dotenv

---

