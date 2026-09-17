# 🎬 Netflix Data Analysis using SQL

<p align="center">
  <img src="https://img.shields.io/badge/SQL-PostgreSQL-336791?style=for-the-badge&logo=postgresql&logoColor=white" />
  <img src="https://img.shields.io/badge/Data%20Analysis-SQL-orange?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Dataset-Netflix-red?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Records-8%2C807-blue?style=for-the-badge" />
  <img src="https://img.shields.io/badge/Business%20Questions-15-green?style=for-the-badge" />
</p>

<h3 align="center">
  📊 Exploratory Data Analysis of Netflix Movies & TV Shows using PostgreSQL
</h3>

<p align="center">
  <i>
    Turning raw Netflix catalogue metadata into structured, business-oriented insights using SQL.
  </i>
</p>

---

## 📌 Project Overview

This project performs **exploratory data analysis on the Netflix Movies and TV Shows catalogue using PostgreSQL**.

The goal was not simply to write SQL queries, but to understand how a real-world dataset can be transformed into meaningful analytical answers through:

**Data → Business Questions → SQL Transformations → Analysis → Interpretation**

The project investigates **15 business-oriented questions** covering:

* 🎬 Movies vs TV Shows
* ⭐ Content ratings
* 🌎 Country-wise content distribution
* 🎭 Genres and cast
* ⏱️ Movie duration
* 📺 TV Show seasons
* 📅 Release-year trends
* 🇮🇳 Indian content
* 🎥 Directors
* 👤 Actors
* 🧹 Missing data
* 🔤 Text-based categorization

The analysis also demonstrates how to work with **messy, semi-structured fields** such as comma-separated countries, directors, cast members, and genres.

---

# 🎯 Business Objective

The project was designed around a simple analytical question:

> **"What can we learn about Netflix's content catalogue using SQL?"**

To answer this, the project explores questions such as:

1. What is the distribution between Movies and TV Shows?
2. Which ratings occur most frequently?
3. Which countries contribute the most content?
4. Which movies have the longest duration?
5. Which TV Shows have more than five seasons?
6. Which genres are most common?
7. How is Indian content distributed across release years?
8. Which directors and actors appear frequently?
9. How complete is the available metadata?
10. What information can be extracted from title descriptions?

---

# 📊 Dataset

### Source

**Netflix Movies and TV Shows Dataset — Kaggle**

🔗 [Netflix Movies and TV Shows Dataset](https://www.kaggle.com/datasets/shivamb/netflix-shows)

The dataset contains:

* **8,807 titles**
* **12 attributes**

The data represents Netflix catalogue metadata rather than individual user behaviour.

---

## 🗂️ Data Dictionary

| Column         | Description                                     |
| -------------- | ----------------------------------------------- |
| `show_id`      | Unique identifier for each title                |
| `type`         | Movie or TV Show                                |
| `title`        | Title of the content                            |
| `director`     | Director or directors associated with the title |
| `cast`         | Cast members associated with the title          |
| `country`      | Country or countries associated with the title  |
| `date_added`   | Date the title was added to Netflix             |
| `release_year` | Original release year                           |
| `rating`       | Content rating                                  |
| `duration`     | Movie duration or number of TV Show seasons     |
| `listed_in`    | Genre/category information                      |
| `description`  | Description of the title                        |

---

# 🏗️ Project Architecture

The project follows a simple SQL analytics pipeline:

```text
                  ┌─────────────────────────┐
                  │   Netflix CSV Dataset   │
                  │     8,807 Titles        │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │    PostgreSQL Table     │
                  │         netflix         │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │   Business Questions    │
                  │          15             │
                  └────────────┬────────────┘
                               │
                               ▼
          ┌─────────────────────────────────────────┐
          │            SQL Transformations           │
          │                                         │
          │ Aggregation │ String Parsing │ Ranking  │
          │ Date Logic  │ CTEs           │ Filters  │
          └────────────────────┬────────────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │   Analytical Results    │
                  └────────────┬────────────┘
                               │
                               ▼
                  ┌─────────────────────────┐
                  │ Business Interpretation │
                  └─────────────────────────┘
```

---

# 📂 Repository Structure

```text
Netflix-Data-Analysis-using-SQL/
│
├── 📄 README.md
├── 📄 Schemas.sql
├── 📄 Business Problems Netflix.sql
├── 📄 Solutions of 15 business problems.sql
└── 📊 netflix_titles.csv
```

### File Description

| File                                    | Purpose                                          |
| --------------------------------------- | ------------------------------------------------ |
| `README.md`                             | Project documentation and analytical methodology |
| `Schemas.sql`                           | PostgreSQL table definition                      |
| `Business Problems Netflix.sql`         | 15 business questions                            |
| `Solutions of 15 business problems.sql` | SQL solutions                                    |
| `netflix_titles.csv`                    | Raw Netflix dataset                              |

---

# 🛠️ Technology Stack

### Database

* PostgreSQL

### Data Format

* CSV

### Tools

* PostgreSQL
* pgAdmin / psql
* Git & GitHub

### SQL Techniques

* `SELECT`
* `WHERE`
* `GROUP BY`
* `ORDER BY`
* `LIMIT`
* `COUNT()`
* `CASE`
* `LIKE`
* `ILIKE`
* `TO_DATE()`
* `CURRENT_DATE`
* `INTERVAL`
* `EXTRACT()`
* `SPLIT_PART()`
* Type Casting
* CTEs
* Subqueries
* Window Functions
* `RANK()`
* `PARTITION BY`
* `STRING_TO_ARRAY()`
* `UNNEST()`

---

# 🔎 Business Problems & SQL Analysis

The project contains **15 analytical problems**, each designed around a specific business question.

---

## 1️⃣ Movies vs TV Shows

### Business Question

> **How many Movies and TV Shows are present in the Netflix catalogue?**

### SQL Concepts

* `GROUP BY`
* `COUNT()`
* Aggregation

### Approach

The dataset is grouped by the `type` column and the number of records in each group is counted.

```text
Netflix Catalogue
       │
       ├── Movies
       │      └── COUNT
       │
       └── TV Shows
              └── COUNT
```

### Analytical Purpose

This establishes the high-level composition of Netflix's catalogue and provides a baseline for subsequent analysis.

---

# 2️⃣ Most Common Rating by Content Type

### Business Question

> **What is the most frequently occurring rating for Movies and TV Shows?**

### SQL Concepts

* CTEs
* `GROUP BY`
* Window Functions
* `RANK()`
* `PARTITION BY`

### Approach

The analysis is performed in two stages.

### Stage 1 — Count ratings

```text
Content Type + Rating
        ↓
COUNT(*)
```

### Stage 2 — Rank ratings

```sql
RANK() OVER (
    PARTITION BY type
    ORDER BY rating_count DESC
)
```

This ranks ratings independently for:

* Movies
* TV Shows

### Why `PARTITION BY`?

Without partitioning, all ratings would be ranked together.

Using:

```sql
PARTITION BY type
```

allows the analysis to answer:

> "What is the most common rating **within each content type**?"

### Why `RANK()`?

If two ratings have the same frequency, both can receive rank 1.

---

# 3️⃣ Content Released in a Specific Year

### Business Question

> **Which titles were released in a specific year, such as 2020?**

### SQL Concepts

* `WHERE`
* Conditional filtering

The `release_year` field is used to filter titles belonging to the selected year.

### Analytical Purpose

This demonstrates basic time-based filtering and enables targeted investigation of catalogue composition for a particular release year.

### Implementation Consideration

If the business question specifically asks for **Movies**, the query should explicitly include:

```sql
type = 'Movie'
```

This highlights an important analytical principle:

> **The SQL implementation must match the exact definition of the business question.**

---

# 4️⃣ Top Countries by Content

### Business Question

> **Which countries are associated with the largest number of Netflix titles?**

### SQL Concepts

* `STRING_TO_ARRAY()`
* `UNNEST()`
* Subqueries
* `GROUP BY`
* `ORDER BY`
* `LIMIT`

### Data Challenge

The `country` field may contain multiple countries in a single row.

Example:

```text
India, United States
```

If the entire string were grouped directly, the database would treat:

```text
India
```

and:

```text
India, United States
```

as completely different categories.

### Transformation

```text
"India, United States"
          ↓
STRING_TO_ARRAY()
          ↓
["India", "United States"]
          ↓
UNNEST()
          ↓
India
United States
```

The resulting values can then be aggregated independently.

### Why It Matters

This demonstrates how to work with **denormalized multi-value fields** using PostgreSQL.

---

# 5️⃣ Longest Movie

### Business Question

> **Which movie has the longest duration?**

### SQL Concepts

* `SPLIT_PART()`
* Type Casting
* `ORDER BY`

### Data Challenge

Movie duration is stored as text:

```text
90 min
120 min
180 min
```

The numeric portion is extracted:

```sql
SPLIT_PART(duration, ' ', 1)
```

and converted into an integer:

```sql
::INT
```

The values can then be sorted numerically.

### Production Improvement

To return only the longest movie, the final query should include:

```sql
LIMIT 1
```

---

# 6️⃣ Content Added Within the Last Five Years

### Business Question

> **Which titles were added to Netflix within the last five years?**

### SQL Concepts

* `TO_DATE()`
* `CURRENT_DATE`
* `INTERVAL`
* Date Arithmetic

### Data Challenge

The source `date_added` field is stored as a string.

Therefore, it needs to be converted into a PostgreSQL date before date comparisons.

Example:

```sql
TO_DATE(date_added, 'Month DD, YYYY')
```

The resulting date can then be compared against:

```sql
CURRENT_DATE - INTERVAL '5 years'
```

### Analytical Purpose

This demonstrates how to perform relative date analysis when source data is not initially stored in a native date format.

---

# 7️⃣ Titles Associated with a Director

### Business Question

> **Which titles are associated with a particular director?**

For example:

```text
Rajiv Chilaka
```

### SQL Concepts

* `STRING_TO_ARRAY()`
* `UNNEST()`
* Subqueries
* Filtering

### Data Challenge

The `director` field can contain multiple directors.

Instead of treating the entire string as one value, the field is split into individual director names.

### Analytical Principle

> **Semi-structured fields often need to be transformed before they can be analyzed effectively.**

---

# 8️⃣ TV Shows with More Than Five Seasons

### Business Question

> **Which TV Shows have more than five seasons?**

### SQL Concepts

* Filtering
* `SPLIT_PART()`
* Type Casting

Example:

```text
8 Seasons
```

is transformed into:

```text
8
```

and converted to an integer.

This makes numerical comparison possible.

---

# 9️⃣ Content Distribution by Genre

### Business Question

> **How many titles are associated with each genre?**

### SQL Concepts

* `STRING_TO_ARRAY()`
* `UNNEST()`
* Aggregation

A single title can belong to multiple genres.

Example:

```text
Dramas, International Movies, Romantic Movies
```

is transformed into:

```text
Dramas
International Movies
Romantic Movies
```

Each genre can then be counted independently.

### Why It Matters

This prevents a multi-genre combination from being treated as one unique category.

---

# 🔟 Indian Content Release-Year Analysis

### Business Question

> **Which release years account for the largest share of Indian catalogue titles?**

### SQL Concepts

* Aggregation
* Subqueries
* Percentage calculation
* Sorting
* `LIMIT`

The analysis calculates the proportion of Indian titles associated with each release year.

Conceptually:

```text
Indian titles in year
--------------------- × 100
Total Indian titles
```

### Important Metric Definition

The original output uses the label:

```text
avg_release
```

However, the underlying calculation represents a **percentage/share**, not an arithmetic average.

A more accurate name would be:

```text
release_share_pct
```

### Analytical Lesson

> **Metric names should accurately represent the mathematical definition of the metric.**

---

# 1️⃣1️⃣ Documentary Content

### Business Question

> **Which titles are classified under the Documentary category?**

### SQL Concepts

* `LIKE`
* Pattern Matching

The `listed_in` field is searched for Documentary-related categories.

### Improvement

If the requirement is specifically documentary **Movies**, the query should also include:

```sql
type = 'Movie'
```

A broader pattern such as:

```sql
LIKE '%Documentaries%'
```

can also be more robust than assuming the category occurs at the end of the field.

---

# 1️⃣2️⃣ Missing Director Information

### Business Question

> **Which titles do not have director information?**

### SQL Concepts

* `IS NULL`

This provides a basic data-quality analysis.

### Why It Matters

Missing values can affect:

* aggregation
* filtering
* reporting
* downstream analysis

Therefore, identifying missing metadata is an important part of exploratory data analysis.

---

# 1️⃣3️⃣ Salman Khan Content Analysis

### Business Question

> **How many titles associated with Salman Khan were released within the last ten years?**

### SQL Concepts

* `LIKE`
* `EXTRACT()`
* Year filtering

The `cast` field is searched for the actor's name and the release year is compared against a rolling ten-year threshold.

### Implementation Improvement

If the question specifically asks for the **number of Movies**, the query should:

```sql
COUNT(*)
```

and include:

```sql
type = 'Movie'
```

This ensures that the output directly matches the business question.

---

# 1️⃣4️⃣ Top Actors in Indian Content

### Business Question

> **Which cast members have the highest number of appearances in titles associated with India?**

### SQL Concepts

* `STRING_TO_ARRAY()`
* `UNNEST()`
* Aggregation
* Sorting
* Top-N analysis

The cast field is split into individual members and their appearances are aggregated.

### Data Consideration

The `country` field can contain multiple countries.

For example:

```text
India, United States
```

would not match:

```sql
country = 'India'
```

A more robust implementation would first split the country field and then check whether India is one of the associated countries.

---

# 1️⃣5️⃣ Rule-Based Description Categorization

### Business Question

> **How many titles contain selected keywords such as `kill` or `violence` in their descriptions?**

### SQL Concepts

* `CASE`
* `ILIKE`
* Pattern Matching
* Aggregation

The query uses conditional logic to create a derived category based on keyword presence.

Conceptually:

```text
Keyword found
     ↓
Category A

No keyword found
     ↓
Category B
```

### Important Limitation

This is **not a machine-learning classifier**.

It is a simple SQL-based keyword rule.

It does not understand:

* Context
* Sentiment
* Semantics
* Negation
* Meaning

Therefore, the result should be interpreted as a **text-processing exercise**, not an objective classification of content quality.

---

# 🧠 SQL Skills Demonstrated

## 1. Aggregation

Used for:

* content counts
* rating frequencies
* country counts
* genre counts
* actor appearances

Key concepts:

```sql
COUNT()
GROUP BY
ORDER BY
```

---

## 2. Common Table Expressions

CTEs allow complex problems to be broken into logical steps.

Example:

```text
Raw Data
   ↓
Aggregated Data
   ↓
Ranked Data
   ↓
Final Result
```

This improves query readability and makes intermediate logic easier to inspect.

---

## 3. Window Functions

The project uses:

```sql
RANK() OVER(...)
```

with:

```sql
PARTITION BY
```

to rank values independently within groups.

---

## 4. String Processing

Important functions include:

```sql
STRING_TO_ARRAY()
UNNEST()
SPLIT_PART()
```

These are used to transform multi-value and semi-structured text fields.

---

## 5. Type Conversion

Examples include:

```sql
::INT
::NUMERIC
```

This is particularly useful when numerical information is embedded inside text fields.

---

## 6. Date Processing

The project uses:

```sql
TO_DATE()
CURRENT_DATE
INTERVAL
EXTRACT()
```

for time-based filtering and analysis.

---

## 7. Conditional Logic

`CASE` is used to create derived categories based on business rules.

---

## 8. Pattern Matching

Both:

```sql
LIKE
```

and:

```sql
ILIKE
```

are used for text-based filtering.

`ILIKE` provides case-insensitive matching in PostgreSQL.

---

# 🧹 Data Challenges & Solutions

One of the most important parts of the project was dealing with the structure of the source dataset.

---

## Challenge 1 — Multi-valued Columns

Fields such as:

```text
country
director
cast
listed_in
```

can contain multiple values in a single row.

### Solution

Use:

```sql
STRING_TO_ARRAY()
```

followed by:

```sql
UNNEST()
```

to transform the data into analyzable rows.

---

## Challenge 2 — Text-Based Duration

Values such as:

```text
120 min
8 Seasons
```

contain both numerical and textual information.

### Solution

Extract the numeric component:

```sql
SPLIT_PART(duration, ' ', 1)
```

and cast it:

```sql
::INT
```

---

## Challenge 3 — Date Stored as Text

The `date_added` field is stored as text.

### Solution

Convert it using:

```sql
TO_DATE()
```

before performing date comparisons.

---

## Challenge 4 — Missing Metadata

Some titles contain missing director information.

### Solution

Use:

```sql
IS NULL
```

to identify incomplete records.

---

# 🏛️ Data Modelling Considerations

The source dataset is not fully normalized.

For example, a single row may contain:

```text
country = India, United States
```

and:

```text
listed_in = Dramas, International Movies
```

For exploratory analysis, these values can be parsed dynamically.

However, in a production database, I would separate these relationships into dedicated tables.

```text
                     netflix_titles
                           │
          ┌────────────────┼────────────────┐
          │                │                │
          ▼                ▼                ▼
   title_country    title_director    title_cast
          │
          ▼
     title_genre
```

This normalized structure would make:

* joins
* filtering
* indexing
* aggregation
* data validation

more reliable and scalable.

---

# ⚙️ Setup & Installation

## Prerequisites

Install:

* PostgreSQL
* pgAdmin or `psql`
* Git

---

## Step 1 — Clone the Repository

```bash
git clone https://github.com/Aasthacoder/Netflix-Data-Analysis-using-SQL.git
```

```bash
cd Netflix-Data-Analysis-using-SQL
```

---

## Step 2 — Create Database

Create a PostgreSQL database:

```sql
CREATE DATABASE netflix_analysis;
```

Connect to the database.

---

## Step 3 — Create the Table

Run:

```text
Schemas.sql
```

This creates the:

```text
netflix
```

table.

---

## Step 4 — Import Dataset

Import:

```text
netflix_titles.csv
```

into the PostgreSQL `netflix` table using pgAdmin's CSV import functionality.

Because the dataset contains commas inside fields such as country, cast, and genres, it should be imported using the CSV parser rather than manually splitting the file.

---

## Step 5 — Review Business Questions

Open:

```text
Business Problems Netflix.sql
```

to review the 15 analytical questions.

---

## Step 6 — Run SQL Solutions

Execute:

```text
Solutions of 15 business problems.sql
```

Each query can be executed independently to inspect its corresponding result.

---

# 📈 Analytical Workflow

The overall analytical process was:

### Step 1 — Understand the dataset

Identify:

* columns
* data types
* categorical fields
* missing values
* multi-valued fields

### Step 2 — Define business questions

Convert general curiosity into specific SQL questions.

### Step 3 — Identify transformation requirements

Examples:

```text
Comma-separated fields → STRING_TO_ARRAY + UNNEST

Text duration → SPLIT_PART + CAST

String date → TO_DATE

Ranking → RANK + PARTITION BY
```

### Step 4 — Write SQL

Use the appropriate SQL operation for each business question.

### Step 5 — Validate interpretation

Check whether:

> **The output actually answers the question being asked.**

### Step 6 — Identify limitations

Consider:

* missing data
* denormalized fields
* metric definitions
* assumptions
* absence of user-level data

---

# ⚠️ Limitations

## 1. No User-Level Behaviour

The dataset does not contain:

* User watch history
* Watch time
* Completion rate
* Click-through rate
* Retention
* Churn
* Subscription information
* User ratings
* Individual engagement

Therefore, this project cannot directly answer:

> "What do Netflix users prefer?"

It answers:

> **"What does the Netflix catalogue contain?"**

---

## 2. Catalogue Size Does Not Equal User Preference

If a genre has a large number of titles, that does not necessarily mean users prefer that genre.

Similarly:

```text
More catalogue content
        ≠
More user engagement
```

---

## 3. Multi-value Fields Are Denormalized

Countries, directors, cast members, and genres may be stored as comma-separated strings.

This requires additional parsing and can create edge cases.

---

## 4. Missing Data

Some metadata fields contain NULL values.

This can affect analyses that depend on complete metadata.

---

## 5. Keyword-Based Categorization

The description-based analysis uses simple keyword matching.

It cannot understand context or meaning.

---

## 6. Metric Definition

Some original analytical labels require clarification.

For example:

```text
avg_release
```

is actually calculated as a percentage share of Indian titles by release year.

Clear metric definitions are essential in professional analytics.

---

# 🛠️ Production-Level Improvements

If this project were developed into a production analytics pipeline, I would implement the following improvements.

### 1. Normalize Multi-valued Attributes

Create separate tables for:

* countries
* directors
* cast
* genres

---

### 2. Improve Data Types

Convert:

```text
date_added → DATE
movie_duration → INTEGER
seasons → INTEGER
```

during ingestion.

---

### 3. Add Data Validation

Introduce checks for:

* duplicate `show_id`
* missing values
* malformed dates
* invalid durations
* unexpected ratings
* inconsistent categories

---

### 4. Improve Query-Business Alignment

Every query should directly match the definition of the business question.

For example:

```sql
type = 'Movie'
```

should be included whenever the question specifically asks about Movies.

---

### 5. Improve Metric Naming

Use names that describe the actual calculation.

For example:

```text
avg_release
```

could be changed to:

```text
release_share_pct
```

---

### 6. Create Reusable Views

Repeated transformations such as country or genre parsing could be implemented as reusable SQL views.

This would reduce repeated logic and improve maintainability.

---

### 7. Extend to User Analytics

If user-level engagement data became available, the project could be extended from catalogue analysis into:

* engagement analysis
* retention analysis
* cohort analysis
* content performance
* regional behaviour
* recommendation analytics

---

# 🚀 Future Scope

The current project answers:

> **What is present in the Netflix catalogue?**

A more advanced version could combine this catalogue data with user engagement data to answer:

> **What content is being consumed, by whom, where, and how does it relate to engagement?**

Potential future analyses include:

### 📺 Content Performance

* Most watched titles
* Watch time by genre
* Completion rate
* Content performance by release year
* Regional content performance

### 👥 User Analytics

* User segmentation
* Cohort analysis
* Retention by content category
* Churn analysis
* Engagement funnels

### 🌎 Regional Analytics

* Country-level consumption
* Regional genre preferences
* Local content performance
* Geographic retention patterns

### 🤖 Recommendation Analytics

Potential recommendation signals could include:

```text
Genre
Country
Rating
Release Year
Watch History
Completion Rate
User Preferences
```

---

# 💡 Key Analytical Lessons

This project reinforced several important data analytics principles.

### 1. Business questions come before SQL

The query should be designed around the question, not the other way around.

### 2. Data structure matters

A technically correct aggregation can still produce misleading results if multi-valued fields are not handled correctly.

### 3. Metric definitions matter

An analyst must understand what a formula actually calculates instead of relying only on a column name.

### 4. Catalogue data has limitations

The number of titles in a category does not automatically indicate user preference or business performance.

### 5. SQL is more than filtering rows

SQL can also be used for:

* transformation
* ranking
* text processing
* date analysis
* data-quality analysis
* business logic

---

# 📌 Project Highlights

| Metric                |               Value |
| --------------------- | ------------------: |
| Dataset Records       |           **8,807** |
| Dataset Attributes    |              **12** |
| Business Questions    |              **15** |
| Database              |      **PostgreSQL** |
| SQL Analysis          | **100% SQL-driven** |
| Window Functions      |                   ✅ |
| CTEs                  |                   ✅ |
| String Processing     |                   ✅ |
| Array Transformation  |                   ✅ |
| Date Processing       |                   ✅ |
| Data Quality Analysis |                   ✅ |

---

# 💼 Skills Demonstrated

### SQL

```text
PostgreSQL
Advanced Filtering
Aggregation
GROUP BY
Subqueries
CTEs
Window Functions
RANK()
PARTITION BY
String Functions
Array Functions
Date Functions
CASE Statements
Pattern Matching
Type Casting
```

### Data Analytics

```text
Exploratory Data Analysis
Business Question Framing
Data Cleaning
Data Transformation
Metric Definition
Data Quality Analysis
Analytical Reasoning
Limitation Analysis
```

### Data Modelling

```text
Relational Schema Design
Handling Denormalized Data
Multi-value Attribute Transformation
Production Data Modelling Considerations
```

---

# 🎓 What This Project Demonstrates

This project demonstrates the ability to move through a complete analytical workflow:

```text
                    BUSINESS QUESTION
                           │
                           ▼
                    UNDERSTAND DATA
                           │
                           ▼
                 IDENTIFY DATA ISSUES
                           │
                           ▼
                  DESIGN SQL LOGIC
                           │
                           ▼
                  TRANSFORM THE DATA
                           │
                           ▼
                AGGREGATE / RANK / FILTER
                           │
                           ▼
                  INTERPRET RESULTS
                           │
                           ▼
                 IDENTIFY LIMITATIONS
                           │
                           ▼
                PROPOSE IMPROVEMENTS
```

The emphasis is not only on producing SQL output, but also on understanding **whether that output represents the intended business question**.

---

# 👩‍💻 Author

## Aastha

**B.Tech — Computational Engineering**
**Indian Institute of Technology Hyderabad**

### Areas of Interest

* Data Analytics
* Product Analytics
* SQL
* Machine Learning
* Product Management

---

# 🔗 Project Links

### GitHub Repository

[Netflix Data Analysis using SQL](https://github.com/Aasthacoder/Netflix-Data-Analysis-using-SQL/)

### Dataset

[Netflix Movies and TV Shows — Kaggle](https://www.kaggle.com/datasets/shivamb/netflix-shows)

---

# ⭐ Final Takeaway

This project started with a simple Netflix catalogue dataset and transformed it into a structured SQL analytics workflow involving **15 business questions**.

The key focus was:

> **Raw Data → SQL Transformation → Business Question → Analytical Result → Critical Interpretation**

Beyond writing queries, the project demonstrates an understanding of:

* data structure
* SQL transformations
* analytical reasoning
* metric definitions
* data-quality issues
* business-question alignment
* limitations of catalogue-level data
* production-level improvement opportunities

---

## 📜 Disclaimer

This project is created for **educational and analytical purposes** using publicly available Netflix catalogue metadata.

The dataset does not represent Netflix's internal user behaviour, recommendation algorithms, financial performance, or proprietary business data.

Therefore, conclusions from this analysis should be interpreted as **catalogue-level observations**, not direct measurements of Netflix user preferences or business performance.
