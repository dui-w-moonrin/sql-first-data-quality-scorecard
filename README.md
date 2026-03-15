# SQL-first Data Quality Scorecard
**WATCHARAPONG “DUI” MOONRIN**

A SQL-first portfolio project that profiles an 11-table relational dataset and exports scorecard-style outputs for validation review.  
This project demonstrates multi-table data quality checks, reconciliation logic, and structured outputs that are easy to review in CSV / Excel-friendly form.

---

## 🚀 Project Overview

This repository shows how I turn raw relational data into a **data quality scorecard** for validation and issue review.

The project focuses on:

- profiling related tables with SQL
- checking completeness, duplicates, sanity flags, and referential integrity
- separating **missing foreign keys (NULL)** from **true orphan records**
- exporting scorecard outputs for downstream review and prioritization

---

## 🎯 Project Objectives

- Build a **SQL-first data quality scorecard** across 11 related tables
- Generate **table-level validation outputs** that are easy to inspect
- Add **cross-table reconciliation logic** for foreign key relationships
- Produce **repeatable artifacts** that support validation / UAT-style review

---

## ✅ What This Project Demonstrates

- **SQL-first profiling** across multiple related tables
- **Data quality checks**: completeness, PK duplicates, sanity flags, referential integrity
- **Reconciliation logic**: distinguish `FK NULL` from `true orphan` cases
- **Structured outputs** for issue prioritization and review
- **Documentation mindset** through ERD, flow, and supporting notes

---

## 🧰 Tools Used

### Major
- **PostgreSQL** — profiling queries, scorecard logic, reconciliation checks
- **Python** — helper scripts for repeatable outputs
- **DBeaver / VS Code**
- **Git**

### Supporting
- **CSV / Excel-friendly outputs** for quick inspection
- **Markdown docs** for reproducibility and explanation

---

## 📦 Key Deliverables

- `artifacts/scorecard.csv` — raw scorecard export
- `artifacts/scorecard_100.csv` — scorecard with `dq_score_0_100`
- `docs/` — ERD, flow/lineage, how-to, exception notes
- `images/` — project visuals and reference diagrams

---

## 📂 Repository Structure

- `raw_data/` — source CSV files
- `sql/` — setup and validation / scorecard SQL
- `python/` — helper scripts
- `docs/` — ERD, flow, reproducibility notes, exception details
- `artifacts/` — generated outputs
- `images/` — project images and diagrams

---

## 🗂 Dataset Source

This project uses a public Kaggle dataset containing 11 related tables across orders, customers, products, suppliers, inventory transactions, and payments.

**Source:**  
[Underwear Data with 11 Tables and up to 100k Rows](https://www.kaggle.com/datasets/hserdaraltan/underwear-data-with-11-tables-and-up-to-100k-rows)

---

## 🧠 Why This Matters

Before reporting or downstream analysis can be trusted, the data needs to be checked first.

This project reflects that workflow by helping answer questions like:

- Do related tables join correctly?
- Are there duplicate or suspicious records?
- Are foreign key issues caused by **missing values** or **broken references**?
- Which tables should be reviewed first?

The goal is not just to “profile data,” but to turn findings into **structured validation evidence** that is easier to explain, review, and prioritize.

---

## 🖼 ER Diagram Preview

![ER Diagram](/images/er_kaggle_as_is.png "ER Diagram")

Full details: `docs/03_er_full_as_is.md`

---

## 📊 Scorecard Preview

| table_name | row_count | overall_null_pct | pk_duplicate_rows | fk_orphan_rows | dq_score_0_100 |
|-----------|----------:|-----------------:|------------------:|---------------:|---------------:|
| customers | 225 | 0.22 | 0 | 0 | 100 |
| inventory_transactions | 20,951 | 24.63 | 0 | 0 | 80 |
| order_details | 105,757 | 0.00 | 0 | 0 | 100 |
| orders | 2,286 | 0.05 | 0 | 0 | 100 |
| payments | 686 | 0.06 | 0 | 0 | 100 |
| products | 4,183 | 7.08 | 0 | 0 | 94 |

**Full outputs**
- `artifacts/scorecard.csv`
- `artifacts/scorecard_100.csv`

---

## 🔎 Validation Focus

This project goes beyond basic null counting.

It also separates:

- **FK NULL rows** → the relationship is unknown / missing
- **Orphan rows** → the foreign key exists but the parent record is missing

That distinction makes validation findings more useful for review and issue prioritization.

---

## 🪣 Recon Buckets Preview

| Bucket | Relationship | Base Rows | FK NULL Rows | FK Non-NULL Rows | Matched Rows | Orphan Rows | NULL % | Severity |
|--------|--------------|----------:|-------------:|-----------------:|-------------:|------------:|-------:|----------|
| A | `orders.shipping_method_id → shipping_methods.shipping_method_id` | 2,286 | 8 | 2,278 | 2,278 | 0 | 0.35% | Low |
| B | `payments.payment_method_id → payment_methods.payment_method_id` | 686 | 1 | 685 | 685 | 0 | 0.15% | Low |
| C | `inventory_transactions.purchase_order_id → purchase_orders.purchase_order_id` | 20,951 | 3,345 | 17,606 | 17,606 | 0 | 15.97% | High |

**Interpretation**
- **Matched Rows** = FK present and found in parent table
- **Orphan Rows** = FK present but parent record missing
- **FK NULL Rows** = relationship unavailable / unknown

More details: `docs/06_recon_buckets_and_exception_list.md`

---

## 📈 Scoring Logic

`dq_score_0_100` starts at **100** and applies explainable penalties for issues such as:

- completeness problems
- PK nulls / PK duplicates
- sanity flags
- FK orphan ratio
- limited date usability

This score is designed as a **simple review signal** to help prioritize which tables need attention first.

---

## 🔄 Flow & Lineage Preview

![Flowchart overview](/artifacts/diagrams/flowchart_full.png "Flowchart overview")

Full details: `docs/04_flowchart_mermaid.md`

---

## 🧪 How to Reproduce

See:

- `docs/01_import_csv_howto.md`
- `docs/02_scorecard_howto.md`

---

## 📚 Additional Notes

For deeper technical details:

- `docs/03_er_full_as_is.md`
- `docs/04_flowchart_mermaid.md`
- `docs/05_table_stats.md`
- `docs/06_recon_buckets_and_exception_list.md`

---

## 👀 Recruiter-Friendly Summary

If you only scan one section, this project demonstrates:

- **SQL-first data profiling**
- **multi-table validation**
- **reconciliation thinking**
- **CSV / Excel-friendly outputs**
- **structured documentation for review** 