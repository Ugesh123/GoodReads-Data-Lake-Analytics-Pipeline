# GoodReads Data Engineering Pipeline

An end-to-end data engineering pipeline for ingesting, transforming, warehousing, validating, and analyzing GoodReads data.

## Architecture

GoodReads Data
    ↓
Landing Zone
    ↓
Working Zone
    ↓
Spark ETL
    ↓
Processed Zone
    ↓
Staging Tables
    ↓
Warehouse Tables
    ↓
Data Quality Checks
    ↓
Analytics Tables

## Pipeline Flow

- GoodReads data is collected and stored in the landing layer.
- Data is moved into a working layer for processing.
- Apache Spark performs dataset transformations and repartitioning.
- Transformed data is written to the processed layer.
- Processed data is loaded into staging tables.
- Warehouse tables are updated using an UPSERT workflow.
- Data quality checks are performed on warehouse tables.
- Analytics tables are generated for author and book analysis.

## Datasets

The pipeline works with four main datasets:

- Authors
- Books
- Reviews
- Users

## Technology Stack

- Python
- Apache Spark / PySpark
- Apache Airflow
- SQL
- PostgreSQL-compatible database connectivity
- AWS S3
- Amazon Redshift
- psycopg2
- boto3

## Data Warehouse

The warehouse contains separate tables for:

- Authors
- Reviews
- Books
- Users

Primary keys are used to identify records and the pipeline uses a staging-to-warehouse update workflow.

## Data Quality

Data quality checks are executed after warehouse loading and again for selected analytics tables.

## Analytics

The pipeline creates analytical datasets for:

- Author reviews
- Author ratings
- Best authors
- Book reviews
- Book ratings
- Best books

## Project Structure

```text
airflow/
    dags/
    plugins/

goodreadsfaker/
    generate_fake_data.py

SampleData/
    author.csv
    book.csv
    reviews.csv
    user.csv

src/
    goodreads_driver.py
    goodreads_transform.py
    goodreads_udf.py
    s3_module.py
    warehouse/

docs/