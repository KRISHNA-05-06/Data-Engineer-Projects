# 👋 Hi, I'm Sri Krishna Sai Kota

**Data & AI Engineer** | Python · PySpark · Kafka · Snowflake · AWS · dbt | Building AI-Integrated Data Pipelines | MS CS @ USF

📍 Tampa, FL (Open to Relocate)  
📧 srikrishnasaikota1@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/srikrishnasai/) · [GitHub](https://github.com/KRISHNA-05-06)

---

## 🗂️ Data Engineering Projects

A curated collection of production-grade data engineering and AI/ML pipeline projects spanning streaming, cloud, healthcare, and LLM integration. Each project is built with real-world scale, observability, and CI/CD in mind.

---

### 1. 🌊 OncoLake — Snowflake Clinical Research Data Platform
**[→ View Repository](https://github.com/KRISHNA-05-06/oncolake)**

A HIPAA-aware, Snowflake-native data platform built on fully synthetic oncology data. It ingests clinical data through multiple paths (Matillion ELT, Snowpipe auto-ingest, and semi-structured JSON), extracts structured fields from free-text clinical notes with an LLM, models the result into governed dimensional marts with dbt (including an SCD Type 2 patient dimension), and surfaces cohort metrics in a Streamlit-in-Snowflake app. Built on the same engineering principles as Moffitt Cancer Center's published clinical data platform — same architecture, applied to synthetic data.

| Detail | Value |
|---|---|
| **Ingestion paths** | Snowpipe (event-driven) + Matillion (orchestrated) into one warehouse |
| **Modeling** | dbt staging + marts, SCD Type 2 patient dimension, 5/5 data-quality tests passing |
| **LLM extraction** | Stage, site, and treatment abstracted from clinical notes (Claude API; Cortex-native version included) |
| **Architecture** | Multi-source → RAW → STAGING (LLM + DQ gate) → dbt marts (SCD2) → Streamlit cohort explorer |

**Tech Stack:**  
`Snowflake` `Matillion` `Snowpipe` `dbt` `AWS (S3, SQS, Lambda, Secrets Manager, IAM)` `Anthropic Claude API` `Snowflake Cortex` `Streamlit-in-Snowflake` `Apache Airflow` `GitHub Actions`

**Highlights:**
- Wired event-driven ingestion end to end — S3 object-create → SQS → Snowpipe auto-load — including the Snowflake–AWS IAM storage-integration handshake, and built a parallel Matillion ELT path (orchestration + transformation jobs) so the same data lands two ways with each path's lineage visible
- Ran LLM extraction over free-text clinical notes into schema-conformant JSON, then modeled it in dbt into a cohort data mart with an SCD Type 2 patient dimension that preserves stage progression over time
- Enforced HIPAA-aware data quality with dbt tests (not-null keys, unique diagnosis IDs, valid AJCC stages) and surfaced cohort metrics and fill-rate checks in a native Streamlit-in-Snowflake explorer
- Documented an evidence-backed query-tuning finding on when Snowflake clustering helps versus hurts (low vs. high cardinality, reclustering cost), read directly from the Query Profile

---

### 2. 🏥 Oncology Clinical-Notes Extraction Pipeline (Claude + Airflow + Snowflake + dbt)
**[→ View Repository](https://github.com/KRISHNA-05-06/oncology-notes-extraction)**

An end-to-end healthcare data engineering pipeline that turns unstructured oncology clinical notes into governed, analytics-ready structured data. Notes are de-identified (HIPAA Safe Harbor), abstracted into a fixed schema using the Claude API, quality-gated, and modeled in Snowflake with dbt — benchmarked against a rule-based NLP baseline so every accuracy claim is measured.

| Detail | Value |
|---|---|
| **Claude micro-F1** | 0.908 (vs 0.884 rule-based baseline) |
| **Biomarker extraction F1** | 1.000 (vs 0.526 baseline) |
| **PHI Redaction** | 2.6 identifiers/note scrubbed pre-extraction |
| **Architecture** | Generate → De-identify → Extract (Claude + baseline) → DQ Gate → Snowflake → dbt |

**Tech Stack:**  
`Anthropic Claude API` `Apache Airflow` `Snowflake` `dbt` `Python` `PyYAML` `ICD-O-3` `HIPAA Safe Harbor`

**Highlights:**
- Abstracts free-text oncology notes into structured JSON (diagnosis, TNM stage, biomarkers, medications, ECOG status) using the Claude API, achieving micro-F1 of 0.908 vs 0.884 for a rule-based baseline
- Demonstrates LLM lift on non-formulaic clinical phrasing — biomarker extraction F1 of 1.000 vs 0.526, correctly parsing variants like `HER2 3+` and `EGFR exon 19 deletion` that regex misses
- Enforces HIPAA Safe Harbor de-identification as a hard gate before extraction, plus a data-quality gate asserting site fill-rate, valid AJCC stages, and zero PHI leakage before load
- Standardizes primary sites to ICD-O-3 registry codes via a dbt seed join, with Snowflake VARIANT landing flattened into cohort-ready analytics marts

---

### 3. 🔴 Real-Time AI Event Intelligence Pipeline
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

### 4. ✈️ Production Airflow ETL Pipelines
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

### 5. ☁️ Airflow on AWS ECS Fargate (Cloud Deployment)
**[→ View Repository](https://github.com/KRISHNA-05-06/airflow-aws-deployment)**

A production-grade cloud deployment that takes Apache Airflow from a local Docker setup to a fully serverless, cloud-native orchestration system on AWS — custom image, managed metadata store, load-balanced UI, and S3 output.

| Detail | Value |
|---|---|
| **Compute** | AWS ECS Fargate (serverless, 4 components) |
| **Metadata Store** | Amazon RDS PostgreSQL |
| **Public Access** | Application Load Balancer |
| **Pipeline Output** | Transformed CSV → Amazon S3 |

**Tech Stack:**  
`Apache Airflow 3.0` `AWS ECS Fargate` `Amazon ECR` `Amazon RDS` `Amazon S3` `Application Load Balancer` `Docker` `Python` `AWS CLI`

**Highlights:**
- Built and pushed a custom Airflow 3.0 Docker image to Amazon ECR, then deployed all four components (api-server, scheduler, triggerer, dag-processor) as serverless ECS Fargate tasks
- Backed Airflow with Amazon RDS PostgreSQL for metadata and exposed the UI publicly through an Application Load Balancer, with the end-to-end DAG uploading transformed output to S3
- Diagnosed and resolved a production deployment failure by tracing repeated ALB health-check timeouts to a missing security group rule (port 8080), reinforcing systematic network-path debugging

---

### 6. ☁️ Airflow on GCP Compute Engine (Multi-Cloud Deployment)
**[→ View Repository](https://github.com/KRISHNA-05-06/airflow-gcp-deployment)**

The GCP counterpart to the AWS deployment above — the same Airflow ETL pipeline deployed with a deliberately different architecture: a single Compute Engine VM running docker-compose, with output to Google Cloud Storage. Demonstrates portable Airflow/Docker skills across two clouds.

| Detail | Value |
|---|---|
| **Compute** | GCP Compute Engine VM (Ubuntu 24.04 LTS, e2-medium) |
| **Metadata Store** | PostgreSQL (containerized) |
| **Auth** | Service account via metadata server (no key files) |
| **Pipeline Output** | Transformed CSV → Google Cloud Storage |

**Tech Stack:**  
`Apache Airflow 3.0` `GCP Compute Engine` `Google Cloud Storage` `Docker` `Docker Compose` `Python` `gcloud CLI`

**Highlights:**
- Deployed all four Airflow components plus PostgreSQL as containers on a single Compute Engine VM via docker-compose, exposing the UI through a firewall-restricted port and persisting output to a GCS bucket
- Implemented keyless GCS authentication using the VM's attached service account through the metadata server, avoiding service-account key files entirely
- Tuned the Airflow 3 API server to a single Uvicorn worker to prevent a memory-driven crash loop on the 4 GB VM, and contrasted the VM-based architecture against the managed AWS ECS approach

---

### 7. 🤖 AI-Powered Job Scraping & Alert System
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

### 8. ⚡ PySpark ETL Pipeline Optimization
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

### 9. 🛒 Grocery ETL Pipeline (PySpark)
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

### 10. 🐳 Containerized ETL Pipeline (Docker + PostgreSQL)
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
| **Cloud** | AWS (S3, ECS Fargate, ECR, RDS, Glue, Lambda, EC2, EMR, SQS, Secrets Manager), GCP (Compute Engine, Cloud Storage, IAM) |
| **Ingestion & ELT** | Matillion, Snowpipe, Streams & Tasks |
| **Orchestration** | Apache Airflow, dbt |
| **ML / AI** | Claude API, Snowflake Cortex, LLM Structured Extraction, Scikit-learn, Isolation Forest, Hugging Face |
| **DevOps** | Docker, GitHub Actions, CI/CD |
| **Databases** | PostgreSQL, MySQL, MongoDB |

---

## 🎓 Education & Certifications

**M.S. Computer Science** — University of South Florida (May 2026)
**B.Tech. Computer Science** — R.V.R & J.C College of Engineering (May 2024)

**Certifications (Anthropic / Skilljar):**
- Building with the Claude API
- Claude with Amazon Bedrock
- Claude with Google Cloud Vertex AI
- Introduction to Model Context Protocol (MCP)
- Dataquest Data Engineer Certification

---

## 💼 Experience Snapshot

**Data Engineer — Prospect Infosystem Inc.** *(May 2021 – Jul 2024)*  
Client: DBS Bank (banking / financial services). Designed and implemented scalable ETL pipelines on AWS (S3, Glue, Spark, Redshift, Athena) processing 200M+ financial records daily, orchestrated 100+ ETL jobs with Apache Airflow and IBM Tivoli Workload Scheduler, and translated business validation rules into Hive-based dimensional data marts for regulatory and analytical reporting.

---

> 💡 *All projects are original, production-grade builds — not tutorials. Built to demonstrate real-world scale, observability, and engineering depth.*

---

*📬 Open to Data Engineer, AI Engineer, and ML Engineer roles. Feel free to reach out!*
