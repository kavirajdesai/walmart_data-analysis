# 🛒 Walmart Data Analysis — End-to-End Analytics Pipeline

> Python · MySQL · SQLAlchemy · Pandas · NumPy · Kaggle API

A structured, end-to-end data analytics pipeline built to extract
meaningful business insights from Walmart's retail sales data. This
project covers the full analytics workflow — from raw data acquisition
to SQL-powered business intelligence — simulating how a data analyst
operates in a real business environment.

---

## 📌 Project Objectives

- Build a reproducible end-to-end analytics pipeline from scratch
- Clean, enrich, and structure raw retail data for analysis
- Load processed data into MySQL for advanced querying
- Answer real business questions about sales, profitability, and
  customer behavior using SQL
- Surface actionable insights that support data-driven decisions

---

## 📊 Key Business Questions Answered

- Which branches are generating the highest revenue?
- What product categories are the best sellers by volume and profit?
- Which day of the week is the busiest for each branch?
- What shift — Morning, Afternoon, or Evening — drives the most
  transactions per branch?
- What are the customer purchasing behavior and payment patterns?

---

## 🗂️ Project Workflow
```
Data Acquisition (Kaggle API)
↓
Data Loading & Exploration (Pandas)
↓
Data Cleaning & Validation
↓
Feature Engineering
↓
Database Integration (MySQL + SQLAlchemy)
↓
SQL Business Analysis
↓
Insights & Findings
```

---

## 📥 1. Data Loading & Exploration

Dataset pulled from Kaggle — 10,051 transactional records across
multiple Walmart branches, product categories, and customer segments.
Initial exploration using `df.shape`, `df.head()`, and `df.describe()`
to understand structure, data types, and statistical distribution.

![Data Loading & Exploration](screenshots/walmart1.jpg)

---

## 🧹 2. Data Cleaning & Feature Engineering

Performed using **Pandas** and **NumPy**:
- Removed `$` symbols from `unit_price` and converted to float
- Handled missing values and duplicate records
- Standardized column names and data types
- Validated numerical fields for consistency

**Feature Engineering — new derived columns:**
- `total` — `unit_price × quantity` for revenue calculation
- `time_of_day` — Morning / Afternoon / Evening from timestamp
- `day_name` — extracted day of week from date
- `month_name` — extracted month for trend analysis

After cleaning, data exported to `walmart_clean_data.csv` and loaded
into MySQL using SQLAlchemy for structured querying.

![Feature Engineering & MySQL Integration](screenshots/walmart2.jpg)

---

## 🗄️ 3. Database Integration

Loaded cleaned data into **MySQL** using **SQLAlchemy**:
```python
engine_mysql = create_engine(
    "mysql+pymysql://user:password@localhost/walmart_db"
)
df.to_sql(name='walmart', con=engine_mysql,
          if_exists='append', index=False)
```
9,969 records successfully loaded into MySQL — enabling efficient,
indexed SQL queries for business analysis.

---

## 🔍 4. SQL Business Analysis

### Busiest Day Per Branch
Used a **window function** (`RANK() OVER PARTITION BY`) to identify
the peak transaction day for each branch without filtering out other
days — a subquery approach that reflects real analytical workflows.

![Busiest Day Per Branch](screenshots/walmart3.jpg)

---

### Sales by Shift — Morning / Afternoon / Evening
Used `CASE WHEN` with `HOUR()` to categorize transactions by time
of day and count invoices per shift per branch — surfacing when each
branch is most operationally active.

![Sales by Shift](screenshots/walmart4.jpg)

---

## 💡 Key Insights

- **Peak Shift** — Afternoon (12PM–5PM) consistently recorded the
  highest invoice count across all branches
- **Busiest Days** — Thursday dominated for WALM001 and WALM002;
  Tuesday peaked for WALM003 with 33 transactions
- **Branch Performance** — Transaction volume varied significantly
  across branches, highlighting staffing and inventory opportunities
- **Feature Engineering Impact** — Deriving `total`, `time_of_day`,
  and `day_name` unlocked analytical questions not answerable from
  the raw dataset alone

---

## 🛠️ Tech Stack

| Tool | Purpose |
|------|---------|
| Python 3.x | Core programming language |
| Pandas | Data cleaning and manipulation |
| NumPy | Numerical operations |
| SQLAlchemy | Python-MySQL ORM integration |
| MySQL | Relational database and SQL analysis |
| Kaggle API | Automated dataset acquisition |
| Jupyter Notebook | Development and documentation |

---

## 📁 Project Structure
```
walmart-data-analysis/
├── walmart_analysis.ipynb     # Main analysis notebook
├── walmart_queries.sql        # All SQL business queries
├── walmart_clean_data.csv     # Cleaned dataset
├── requirements.txt           # Python dependencies
├── screenshots/               # Query and output screenshots
└── README.md
```
---

## ⚙️ Installation & Setup

**1. Clone the repository:**
git clone https://github.com/kavirajdesai/walmart-data-analysis.git
cd walmart-data-analysis

**2. Install dependencies:**
pip install -r requirements.txt

**3. Configure Kaggle API:**
- Go to kaggle.com → Account → Create API Token
- Place `kaggle.json` in `~/.kaggle/`
- Run the dataset download command from the notebook

**4. Configure MySQL:**
- Create a database called `walmart_db`
- Update the connection string in the notebook with your credentials

**5. Run the notebook:**
jupyter notebook walmart_analysis.ipynb

---

## 📚 Skills Demonstrated

- End-to-end data pipeline construction
- Data cleaning and feature engineering with Pandas
- Relational database design and MySQL integration
- Advanced SQL — window functions, CASE WHEN, subqueries,
  GROUP BY, RANK()
- Translating raw data into actionable business insights
- API-based data acquisition with Kaggle

---

## 👨‍💻 Author

**Kaviraj Desai**
- LinkedIn: [linkedin.com/in/kavirajdesai](https://linkedin.com/in/kavirajdesai)
- GitHub: [github.com/kavirajdesai](https://github.com/kavirajdesai)
