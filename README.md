# 👋 Hi, I'm Sri Krishna Sai Kota

**Data & AI Engineer** | Python · PySpark · Kafka · Snowflake · AWS · dbt | Building AI-Integrated Data Pipelines | MS CS @ USF

📍 Tampa, FL (Open to Relocate)  
📧 srikrishnasaikota1@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/srikrishnasai/) · [GitHub](https://github.com/KRISHNA-05-06)

---

## 🗂️ Data Engineering Projects

A curated collection of production-grade data engineering and AI/ML pipeline projects. Each project is built with real-world scale, observability, and CI/CD in mind.

---

### 1. 🔴 Real-Time AI Event Intelligence Pipeline
**[→ View Repository](https://github.com/KRISHNA-05-06/realtime-ai-pipeline)**

A fully containerized, end-to-end real-time streaming pipeline that ingests high-volume events, detects anomalies with ML, and classifies intent using LLMs — all running across 13 Docker services.

| Detail | Value |
|---|---|
| **Events Processed** | 1.5M+ |
| **Anomaly Detection F1** | 0.896 (Isolation Forest) |
| **CI/CD Tests** | 21/21 passing |
| **Architecture** | Producer → Kafka → ClickHouse → Isolation Forest + LLM |

**Tech Stack:**  
`Apache Kafka` `ClickHouse` `Python` `Docker` `Isolation Forest` `LLM Intent Classification` `CI/CD` `GitHub Actions`

**Highlights:**
- Ingests and processes 1.5M+ events with sub-second latency using Kafka topics and consumer groups
- Detects anomalies in real time using Isolation Forest (F1 = 0.896) and classifies event intent via LLM pipeline
- Deployed across 13 Docker services with full CI/CD automation and 21/21 test coverage

---

### 2. ✈️ Production Airflow ETL Pipelines
**[→ View Repository](https://github.com/KRISHNA-05-06/airflow_dags)**

Two production-grade Apache Airflow ETL pipelines built with Docker, MySQL, git-sync auto-deployment, and GitHub Actions CI/CD — mirroring real-world data engineering team workflows.

| Detail | Value |
|---|---|
| **Pipelines** | Daily Market Data ETL + Books Data ETL |
| **Books Extracted** | 50 real titles via Open Library API |
| **DAG Deployment** | Automatic via git-sync (every 30s) |
| **CI/CD** | GitHub Actions DAG validation on every push |

**Tech Stack:**  
`Apache Airflow 3.0` `Docker` `MySQL` `git-sync` `GitHub Actions` `Python` `Open Library API` `XCom`

**Highlights:**
- Built a multi-region market data pipeline using Airflow's dynamic task mapping with `.expand()`, running 4 parallel Extract → Transform → Load chains simultaneously
- Extracted 50 real data engineering books via Open Library API, applying type conversion, deduplication, and timestamp enrichment before loading into MySQL with a truncate-and-insert idempotency pattern
- Configured git-sync sidecar container for automatic DAG deployment from GitHub every 30 seconds, eliminating manual restarts; added GitHub Actions CI to validate all DAG syntax before deployment

---

### 3. 🤖 AI-Powered Job Scraping & Alert System
**[→ View Repository](https://github.com/KRISHNA-05-06/ai-job-hunter)**

An automated multi-platform job intelligence system that scrapes job postings 5x daily, scores them with AI, and delivers personalized HTML email alerts — without requiring a laptop to be running.

| Detail | Value |
|---|---|
| **Platforms Scraped** | LinkedIn, Indeed, Dice, Glassdoor |
| **Frequency** | 5x daily via GitHub Actions |
| **AI Model** | Groq / Llama |
| **Delivery** | HTML Email Alerts |

**Tech Stack:**  
`Python` `Groq API` `Llama` `GitHub Actions` `BeautifulSoup / Scrapy` `SMTP` `Docker`

**Highlights:**
- Scrapes 4 major job platforms on a scheduled cron and deduplicates listings across sources
- Uses Groq/Llama to score job relevance against a skills profile and filter low-match postings
- Delivers formatted HTML digest emails automatically, fully serverless via GitHub Actions

---

### 4. ⚡ PySpark ETL Pipeline Optimization
**[→ View Repository](https://github.com/KRISHNA-05-06/PySpark-ETL-Pipeline-Optimization)**

A hands-on performance tuning project that diagnoses and resolves real bottlenecks in a PySpark ETL pipeline — achieving a 61% runtime reduction using systematic optimization techniques.

| Detail | Value |
|---|---|
| **Baseline Runtime** | 47 seconds |
| **Optimized Runtime** | ~18 seconds |
| **Performance Gain** | 61% improvement |
| **Monitoring** | Spark UI (localhost:4040) |

**Tech Stack:**  
`PySpark` `Docker` `Parquet` `Spark UI`

**Highlights:**
- Diagnosed bottlenecks using Spark UI: redundant `.count()` actions, 200 partitions for 75 records, and repeated full scans without caching
- Applied predicate pushdown, strategic DataFrame caching, coalesce-based repartitioning, and combined aggregations into a single `.agg()` pass
- Reduced partition count from 200 to 1 and eliminated excessive small file generation, cutting overhead significantly

---

### 5. 🛒 Grocery ETL Pipeline (PySpark)
**[→ View Repository](https://github.com/KRISHNA-05-06/PySpark-ETL-Pipeline)**

A complete Extract-Transform-Load pipeline built with PySpark that ingests messy, multi-source sales data and produces clean, analytics-ready output — handling real-world data quality issues end to end.

| Detail | Value |
|---|---|
| **Data Sources** | Online, Store, Mobile orders |
| **Spark Version** | Spark 4.0 |
| **Input Format** | Multi-format CSV (mixed dates, dirty prices, duplicate records) |
| **Output** | Cleaned Parquet / CSV with validation report |

**Tech Stack:**  
`PySpark` `Python` `Spark SQL` `Pandas` `Logging`

**Highlights:**
- Ingested and unified 3 order sources using `unionByName` with explicit schema and `PERMISSIVE` mode to handle malformed rows without data loss
- Standardized mixed date formats, stripped price symbols, normalized customer IDs, and removed test/duplicate records using Spark DataFrame transformations
- Implemented Spark SQL validation checks (zero-price detection, date range verification, record count) and generated a summary report with revenue and regional distribution metrics

---

### 6. 🐳 Containerized ETL Pipeline (Docker + PostgreSQL)
**[→ View Repository](https://github.com/KRISHNA-05-06/python-postgres-etl-pipeline)**

A production-style ETL demo showcasing Docker best practices — multi-stage builds, health checks, non-root users, and environment-based config — containerizing a Python-to-PostgreSQL data pipeline.

| Detail | Value |
|---|---|
| **Services** | PostgreSQL 15 + Python ETL app |
| **Container Pattern** | Multi-stage Docker build |
| **Config** | Environment-variable driven (.env) |
| **Storage** | Persistent named Docker volume |

**Tech Stack:**  
`Python` `PostgreSQL` `Docker` `Docker Compose` `psycopg2`

**Highlights:**
- Built a two-service Docker Compose stack with a PostgreSQL health check and `depends_on: service_healthy` to guarantee database readiness before the ETL app starts
- Applied multi-stage Dockerfile to minimize image size and ran the application container as a non-root user for improved security posture
- Structured environment-based configuration using `.env` and `.env.example` for safe, portable secret management across environments

---

## 🛠️ Core Technical Skills

| Category | Tools |
|---|---|
| **Languages** | Python, SQL, Bash |
| **Streaming** | Apache Kafka, Kafka Streams |
| **Data Warehousing** | Snowflake, ClickHouse, Redshift |
| **Big Data** | PySpark, Hadoop |
| **Cloud** | AWS (S3, Glue, Lambda, EC2, EMR), GCP |
| **Orchestration** | Apache Airflow, dbt |
| **ML / AI** | Scikit-learn, Isolation Forest, LLM APIs, Hugging Face |
| **DevOps** | Docker, GitHub Actions, CI/CD |
| **Databases** | PostgreSQL, MySQL, MongoDB |

---

## 🎓 Education & Certifications

**M.S. Computer Science** — University of South Florida (May 2026)  
**B.Tech Computer Science** — R.V.R & J.C College of Engineering (2024)

**Certifications (Anthropic / Skilljar):**
- Building with the Claude API
- Claude with Amazon Bedrock
- Claude with Google Cloud Vertex AI
- Introduction to Model Context Protocol (MCP)
- Dataquest Data Engineer Certification

---

## 💼 Experience Snapshot

**Data Engineer Intern — Magnum Wings** *(May 2023 – Jun 2024)*  
Aviation domain. Built and maintained data pipelines, optimized ETL workflows, and integrated data across operational systems.

**Data Engineer Intern — Prospect Infosystem Inc.** *(May 2022 – Apr 2023)*  
Consulting domain. Developed scalable data solutions and reporting pipelines for enterprise clients.

---

> 💡 *All projects are original, production-grade builds — not tutorials. Built to demonstrate real-world scale, observability, and engineering depth.*

---

*📬 Open to Data Engineer, AI Engineer, and ML Engineer roles. Feel free to reach out!*
