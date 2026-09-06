## Financial Database & Revenue Analysis System

End-to-end financial data analysis using SQL and Power BI to uncover transaction trends, customer behavior, account activity, and revenue performance.

# Financial Database & Revenue Analysis System

![MySQL](https://img.shields.io/badge/Database-MySQL-blue)
![SQL](https://img.shields.io/badge/Language-SQL-orange) ![Project
Type](https://img.shields.io/badge/Project-Data%20Analytics-green)

## Table of Contents

* [1. Project Overview](#1-project-overview)
* [2. Project Purpose](#2-project-purpose)
* [3. Business Problem](#3-business-problem)
* [4. Project Objectives](#4-project-objectives)
* [5. Database Architecture](#5-database-architecture)
* [6. Database Schema](#6-database-schema)
* [7. Table Documentation](#7-table-documentation)
* [8. Relationships](#8-relationships)
* [9. Data Coverage](#9-data-coverage)
* [10. SQL Techniques Demonstrated](#10-sql-techniques-demonstrated)
* [11. Business Questions Answered](#11-business-questions-answered)
* [12. Analytical Queries](#12-analytical-queries)
* [13. Revenue Analysis](#13-revenue-analysis)
* [14. Customer & Account Analysis](#14-customer--account-analysis)
* [15. Transaction Analysis](#15-transaction-analysis)
* [16. Business Value](#21-business-value)
* [17. Skills Demonstrated](#22-skills-demonstrated)
* [18. Conclusion](#24-conclusion)

---

## 1. Project Overview

The **Financial Database & Revenue Analysis System** is a MySQL-based
data analytics project designed to model a simplified financial
institution and extract business insights from customer, account,
transaction, and revenue data.

The SQL project creates a relational database named `FINANCIAL_DATABASE`
and organizes financial information into four major entities:

1. **Customers** -- stores customer demographic and registration
   information.
2. **Accounts** -- stores customer account details, account types,
   balances, and statuses.
3. **Transactions** -- records deposits, withdrawals, and transfers.
4. **Revenue** -- records revenue generated from fees, interest, loan
   repayments, ATM charges, POS commissions, SMS charges, and other
   sources.

The project goes beyond database creation by using SQL analytical
queries to answer practical business questions around revenue
performance, customer activity, account balances, deposits, withdrawals,
and customer acquisition.

---
<img width="898" height="496" alt="finance 2" src="https://github.com/user-attachments/assets/f2a9f505-7bf2-44e0-9a90-45cd9104927d" />



## 2. Project Purpose

The purpose of this project is to demonstrate how SQL can be used to
move from **structured financial data** to **actionable business
analysis**.

The workflow covers:

**Database creation → Table design → Data insertion → Relational joins →
Aggregation → Time-based analysis → Ranking → Percentage analysis →
Growth analysis**

This makes the project suitable as a portfolio demonstration of
practical SQL and entry-level data analytics skills.

---

## 3. Business Problem

A financial institution generates large volumes of customer and
transaction data. Without a structured database and analytical queries,
it becomes difficult to answer questions such as:

* How much revenue is generated each month?
* Which customers make the largest deposits?
* Which account types maintain the highest average balances?
* Which customers are the most transaction-active?
* What percentage of transactions are deposits versus withdrawals?
* Which revenue sources contribute the most income?
* Is monthly revenue increasing or decreasing?
* Which accounts have the highest transaction activity?
* How many new customers are registered each month?
* How does account balance vary by account opening month?

This project addresses these questions using relational SQL analysis.

---

## 4. Project Objectives

### Primary Objectives

* Build a relational financial database using MySQL.
* Create normalized entities for customers, accounts, transactions,
  and revenue.
* Establish relationships using primary and foreign keys.
* Populate the database with sample financial records.
* Analyze financial activity using SQL.
* Calculate monthly revenue and revenue growth.
* Identify high-value customers based on deposits.
* Compare average balances by account type.
* Measure transaction activity.
* Analyze deposits and withdrawals as percentages of transaction
  activity.
* Identify revenue sources and their contribution.
* Track customer registration trends.
* Prepare the database for BI/dashboard integration.

### Analytical Objectives

The SQL analysis specifically focuses on:

* Revenue performance
* Customer value
* Account performance
* Transaction activity
* Revenue-source contribution
* Customer acquisition
* Account balance trends

---

# 5. Database Architecture

The database follows a relational structure in which customers own
accounts, accounts generate transactions, and accounts are associated
with revenue records.

```text
                    ┌──────────────────────┐
                    │      CUSTOMERS       │
                    ├──────────────────────┤
                    │ PK customer_id       │
                    │ first_name           │
                    │ last_name            │
                    │ gender               │
                    │ date_of_birth        │
                    │ phone_number         │
                    │ email                │
                    │ address              │
                    │ city                 │
                    │ state                │
                    │ registration_date    │
                    └──────────┬───────────┘
                               │
                               │ 1 : Many
                               ▼
                    ┌──────────────────────┐
                    │       ACCOUNTS       │
                    ├──────────────────────┤
                    │ PK account_id        │
                    │ FK customer_id       │
                    │ account_number       │
                    │ account_type         │
                    │ opening_balance      │
                    │ current_balance      │
                    │ account_status       │
                    │ opening_date         │
                    └───────┬────────┬─────┘
                            │        │
                   1 : Many │        │ 1 : Many
                            ▼        ▼
             ┌──────────────────┐  ┌────────────────────┐
             │   TRANSACTIONS   │  │      REVENUE       │
             ├──────────────────┤  ├────────────────────┤
             │ PK transaction_id│  │ PK revenue_id     │
             │ FK account_id    │  │ FK account_id     │
             │ transaction_date │  │ revenue_date      │
             │ transaction_type │  │ revenue_source    │
             │ amount           │  │ amount             │
             │ channel          │  │ notes              │
             │ status           │  └────────────────────┘
             │ description      │
             └──────────────────┘
```

---

# 6. Database Schema

## 6.1 Customers

The `Customers` table stores customer identity, demographic, contact,
location, and registration information.

---

Column                Data Type         Constraint        Description

---

`customer_id`         INT               Primary Key, Auto Unique customer
Increment         identifier

`first_name`          VARCHAR(50)       NOT NULL          Customer first
name

`last_name`           VARCHAR(50)       NOT NULL          Customer last
name

`gender`              ENUM              ---               Male/Female

`date_of_birth`       DATE              ---               Customer date of
birth

`phone_number`        VARCHAR(15)       ---               Customer phone
number

`email`               VARCHAR(100)      UNIQUE            Customer email

`address`             VARCHAR(255)      ---               Customer address

`city`                VARCHAR(50)       ---               Customer city

`state`               VARCHAR(50)       ---               Customer state

`registration_date`   DATE              NOT NULL          Date customer
registered
----------

The SQL script defines `customer_id` as the primary key and `email` as a
unique field. fileciteturn5file1L324-L338

---

## 6.2 Accounts

The `Accounts` table represents customer bank accounts.

---

Column              Data Type         Constraint        Description

---

`account_id`        INT               Primary Key, Auto Unique account
Increment         identifier

`customer_id`       INT               Foreign Key, NOT  Links account to
NULL              customer

`account_number`    VARCHAR(20)       UNIQUE, NOT NULL  Account number

`account_type`      ENUM              NOT NULL          Savings, Current,
Business

`opening_balance`   DECIMAL(15,2)     NOT NULL          Balance when
account was
opened

`current_balance`   DECIMAL(15,2)     NOT NULL          Current recorded
balance

`account_status`    ENUM              DEFAULT Active    Active, Inactive,
Closed

`opening_date`      DATE              NOT NULL          Account opening
date
----

The script uses `customer_id` as a foreign key to connect accounts to
customers. fileciteturn5file1L179-L188

---

## 6.3 Transactions

The `Transactions` table records financial activity performed on
customer accounts.

---

Column                  Data Type         Constraint        Description

---

`transaction_id`        INT               Primary Key, Auto Unique
Increment         transaction
identifier

`account_id`            INT               Foreign Key, NOT  Account involved
NULL              in transaction

`transaction_date`      DATE              NOT NULL          Transaction date

`transaction_type`      ENUM              NOT NULL          Deposit,
Withdrawal,
Transfer

`amount`                DECIMAL(15,2)     NOT NULL          Transaction
amount

`transaction_channel`   ENUM              ---               ATM, Mobile App,
POS, Bank Branch,
Online Banking

`transaction_status`    ENUM              ---               Successful,
Reversed,
Pending, Failed

`description`           VARCHAR(255)      ---               Transaction
description
-----------

The transaction design uses controlled values for transaction type,
channel, and status. fileciteturn5file0L242-L251

---

## 6.4 Revenue

The `Revenue` table captures income associated with financial services
and account activity.

---

Column             Data Type         Constraint        Description

---

`revenue_id`       INT               Primary Key, Auto Unique revenue
Increment         record

`account_id`       INT               Foreign Key, NOT  Related account
NULL

`revenue_date`     DATE              ---               Revenue date

`revenue_source`   ENUM              ---               Source of revenue

`amount`           DECIMAL(15,2)     NOT NULL          Revenue amount

`notes`            VARCHAR(255)      ---               Revenue
description
-----------

Revenue sources defined in the SQL include:

* Transfer Fee
* Maintenance Fee
* Interest
* Loan Repayment
* SMS Charge
* ATM Charge
* Other
* POS Commission
* Cheque book fee

The `Revenue` table is linked to `Accounts` through `account_id`.
fileciteturn4file0L89-L96

---

# 7. Table Documentation

## Customers → Accounts

A customer can own one or more accounts.

```text
Customers.customer_id
        ↓
Accounts.customer_id
```

This relationship allows customer-level analysis such as:

* Total deposits by customer
* Total transactions by customer
* Customer account ownership
* Customer activity ranking

## Accounts → Transactions

An account can have many transactions.

```text
Accounts.account_id
        ↓
Transactions.account_id
```

This supports:

* Transaction counts
* Deposit analysis
* Withdrawal analysis
* Account activity ranking
* Transaction status analysis

## Accounts → Revenue

An account can generate multiple revenue records.

```text
Accounts.account_id
        ↓
Revenue.account_id
```

This supports:

* Monthly revenue analysis
* Revenue by source
* Revenue contribution
* Revenue growth

---

# 8. Relationships

Parent Table   Child Table    Key             Relationship

---

Customers      Accounts       `customer_id`   One-to-Many
Accounts       Transactions   `account_id`    One-to-Many
Accounts       Revenue        `account_id`    One-to-Many

This relational model enables analysis across multiple levels of the
financial system.

For example:

```text
Customer
   ↓
Account
   ↓
Transaction
```

and:

```text
Customer
   ↓
Account
   ↓
Revenue
```

These relationships are particularly important for analytical joins.

---

# 9. Data Coverage

The SQL file contains sample records across multiple entities.

The customer data contains records registered throughout 2024, with many
customer records associated with Port Harcourt, Rivers State. The
accounts data includes Savings, Current, and Business account types.
fileciteturn5file1L345-L378

The account records include opening balances, current balances, account
status, and opening dates. fileciteturn5file0L86-L110

The transaction dataset contains deposits, withdrawals, and transfers
across channels including:

* ATM
* Mobile App
* POS
* Bank Branch
* Online Banking

It also includes multiple transaction outcomes:

* Successful
* Reversed
* Pending
* Failed

These fields make the database suitable for operational and financial
performance analysis. fileciteturn5file0L253-L311

---

# 10. SQL Techniques Demonstrated

This project demonstrates several important SQL concepts.

## Database Management

* `CREATE DATABASE`
* `USE`
* `CREATE TABLE`
* `DROP TABLE`
* `INSERT INTO`
* `SELECT`

## Data Definition

* Primary keys
* Foreign keys
* `AUTO_INCREMENT`
* `NOT NULL`
* `UNIQUE`
* `ENUM`
* `DECIMAL`

## Data Retrieval

* `SELECT`
* `WHERE`
* `ORDER BY`
* `LIMIT`

## Aggregation

* `SUM()`
* `AVG()`
* `COUNT()`
* `ROUND()`

## Grouping

* `GROUP BY`

## Joins

* `JOIN`

## Conditional Analysis

* `CASE WHEN`

## Date Analysis

* `DATE_FORMAT()`

## Window Functions

* `LAG()`

## String Functions

* `CONCAT()`

## Subqueries

* Nested `SELECT` statements

These techniques demonstrate practical SQL for data analysis rather than
only basic querying.

---

# 11. Business Questions Answered

The analytical section of the SQL file addresses the following
questions:

### Revenue

1. What is the total revenue generated each month?
2. How much did revenue grow from one month to the next?
3. What percentage of total revenue comes from each revenue source?

### Customers

4. Which five customers have the highest total deposits?
5. How many new customers registered each month?
6. Which customers have the highest transaction activity?

### Accounts

7. What is the average balance for each account type?
8. How much total balance is associated with accounts opened in each
   month?
9. Which accounts are the most active?

### Transactions

10. What percentage of transactions are deposits?
11. What percentage are withdrawals?
12. Which accounts have the highest transaction counts?

---

# 12. Analytical Queries

## 12.1 Total Revenue by Month

The project uses `DATE_FORMAT()` to group revenue records by year and
month.

```sql
SELECT
    DATE_FORMAT(Revenue_date, '%Y-%m') AS month,
    SUM(R.Amount) AS total_revenue
FROM Revenue r
JOIN Transactions t
    ON Revenue_id = t.transaction_id
JOIN Accounts a
    ON t.account_id = a.account_id
JOIN Customers c
    ON a.customer_id = c.customer_id
GROUP BY DATE_FORMAT(Revenue_date, '%Y-%m')
ORDER BY month;
```

### Analytical purpose

This query measures monthly revenue performance and creates a time
series that can be used for trend analysis.

The original SQL file uses `DATE_FORMAT()` and `SUM()` to produce
monthly revenue totals. fileciteturn3file0L29-L40

---

## 12.2 Top 5 Customers by Deposits

```sql
SELECT
    c.customer_id,
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    SUM(t.amount) AS total_deposits
FROM Customers c
JOIN Accounts a
    ON c.customer_id = a.customer_id
JOIN Transactions t
    ON a.account_id = t.account_id
WHERE t.transaction_type = 'Deposit'
GROUP BY c.customer_id, c.first_name, c.last_name
ORDER BY total_deposits DESC
LIMIT 5;
```

### Analytical purpose

This identifies customers contributing the highest deposit volumes.

Potential business uses include:

* Customer segmentation
* Relationship management
* High-value customer identification
* Deposit strategy

The query is included in the source SQL file and uses joins, filtering,
aggregation, sorting, and `LIMIT`. fileciteturn3file0L43-L55

---

## 12.3 Average Balance by Account Type

```sql
SELECT
    account_type,
    ROUND(AVG(Current_balance), 2) AS average_balance
FROM Accounts
GROUP BY account_type
ORDER BY average_balance DESC;
```

### Analytical purpose

This compares average balances across:

* Savings
* Current
* Business

The query uses `AVG()`, `ROUND()`, `GROUP BY`, and `ORDER BY`.
fileciteturn3file0L57-L62

---

## 12.4 Customers with the Most Transactions

```sql
SELECT
    c.customer_id,
    c.first_name,
    c.last_name,
    COUNT(t.transaction_id) AS total_transactions
FROM Customers c
JOIN Accounts a
    ON c.customer_id = a.customer_id
JOIN Transactions t
    ON a.account_id = t.account_id
GROUP BY
    c.customer_id,
    c.first_name,
    c.last_name
ORDER BY total_transactions DESC;
```

### Analytical purpose

This identifies customers with the highest transaction activity.

It can support:

* Customer engagement analysis
* Digital banking analysis
* Customer segmentation
* Activity monitoring

The source query uses `COUNT()` across the customer-account-transaction
relationship. fileciteturn3file0L64-L78

---

# 13. Revenue Analysis

## 13.1 Monthly Revenue Growth

The project uses the `LAG()` window function to compare each month's
revenue with the previous month.

```sql
SELECT
    DATE_FORMAT(revenue_date, '%Y-%m') AS month,
    SUM(amount) AS total_revenue,

    SUM(amount) -
        LAG(SUM(amount)) OVER (
            ORDER BY DATE_FORMAT(revenue_date, '%Y-%m')
        ) AS revenue_growth,

    ROUND(
        (
            (
                SUM(amount) -
                LAG(SUM(amount)) OVER (
                    ORDER BY DATE_FORMAT(revenue_date, '%Y-%m')
                )
            )
            /
            LAG(SUM(amount)) OVER (
                ORDER BY DATE_FORMAT(revenue_date, '%Y-%m')
            )
        ) * 100,
        2
    ) AS growth_percentage

FROM Revenue
GROUP BY DATE_FORMAT(revenue_date, '%Y-%m')
ORDER BY month;
```

### Metrics generated

* `total_revenue`
* `revenue_growth`
* `growth_percentage`

This is one of the more advanced analytical sections because it uses a
window function to compare a grouped monthly metric against its previous
period. fileciteturn3file2L137-L154

---

## 13.2 Revenue by Source

```sql
SELECT
    revenue_source,
    SUM(amount) AS total_revenue,
    ROUND(
        SUM(amount) * 100.0 /
        (SELECT SUM(amount) FROM Revenue),
        2
    ) AS percentage_contribution
FROM Revenue
GROUP BY revenue_source
ORDER BY total_revenue DESC;
```

### Metrics generated

* Total revenue per source
* Percentage contribution to overall revenue

### Revenue sources

The analysis can compare sources such as:

* Transfer Fee
* Maintenance Fee
* Interest
* Loan Repayment
* SMS Charge
* ATM Charge
* POS Commission
* Cheque Book Fee
* Other

The source SQL calculates contribution using a subquery containing total
revenue. fileciteturn3file2L156-L166

---

# 14. Customer & Account Analysis

## 14.1 Most Active Accounts

```sql
SELECT
    a.account_id,
    a.account_number,
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    COUNT(t.transaction_id) AS transaction_count
FROM Accounts a
JOIN Customers c
    ON a.customer_id = c.customer_id
JOIN Transactions t
    ON a.account_id = t.account_id
GROUP BY
    a.account_id,
    a.account_number,
    c.first_name,
    c.last_name
ORDER BY transaction_count DESC
LIMIT 10;
```

### Purpose

This produces the top 10 accounts based on transaction count.

The query combines three tables and uses `COUNT()`, `GROUP BY`,
`ORDER BY`, and `LIMIT`. fileciteturn3file2L168-L184

---

## 14.2 New Customers per Month

```sql
SELECT
    DATE_FORMAT(registration_date, '%Y-%m') AS month,
    COUNT(customer_id) AS new_customers
FROM Customers
GROUP BY DATE_FORMAT(registration_date, '%Y-%m')
ORDER BY month;
```

### Purpose

This measures customer acquisition over time.

The result can be used to identify:

* High-registration months
* Low-registration months
* Customer acquisition trends
* Growth periods

The query is included in the source SQL file.
fileciteturn3file2L186-L191

---

## 14.3 Total Account Balance by Month

```sql
SELECT
    DATE_FORMAT(opening_date, '%Y-%m') AS month,
    SUM(current_balance) AS total_balance
FROM Accounts
GROUP BY DATE_FORMAT(opening_date, '%Y-%m')
ORDER BY month;
```

### Purpose

This groups current account balances according to account opening month.

It can help examine the balance associated with cohorts of newly opened
accounts. fileciteturn3file2L193-L198

---

# 15. Transaction Analysis

## 15.1 Deposit vs Withdrawal Percentage

```sql
SELECT
    ROUND(
        SUM(
            CASE
                WHEN transaction_type = 'Deposit' THEN 1
                ELSE 0
            END
        ) * 100.0 / COUNT(*),
        2
    ) AS deposit_percentage,

    ROUND(
        SUM(
            CASE
                WHEN transaction_type = 'Withdrawal' THEN 1
                ELSE 0
            END
        ) * 100.0 / COUNT(*),
        2
    ) AS withdrawal_percentage

FROM Transactions
WHERE transaction_type IN ('Deposit', 'Withdrawal');
```

### Purpose

This calculates the percentage of transactions that are deposits and
withdrawals.

### SQL concepts demonstrated

* `CASE WHEN`
* Conditional counting
* `COUNT()`
* Percentage calculation
* `ROUND()`
* `WHERE ... IN`

The original query explicitly filters to deposits and withdrawals before
calculating the percentages.

---

# 21. Business Value

This project demonstrates how a financial organization can use
structured data to support operational and strategic decision-making.

## Revenue Management

Management can identify:

* High-performing revenue sources
* Revenue trends
* Revenue growth or decline
* Revenue concentration

## Customer Management

The analysis can help identify:

* High-value deposit customers
* Highly active customers
* Customer acquisition trends
* Potential customer segments

## Account Management

The database can support analysis of:

* Account types
* Account balances
* Account activity
* Account status

## Transaction Monitoring

The transaction table provides a foundation for analyzing:

* Transaction volumes
* Transaction channels
* Transaction statuses
* Deposits
* Withdrawals
* Transfers

---

# 22. Skills Demonstrated

This project demonstrates practical skills in:

### SQL

* Database creation
* Relational database design
* Table creation
* Data insertion
* Primary and foreign keys
* Joins
* Aggregations
* Filtering
* Grouping
* Sorting
* Conditional logic
* Subqueries
* Date functions
* Window functions

### Data Analytics

* KPI definition
* Revenue analysis
* Customer analysis
* Account analysis
* Transaction analysis
* Trend analysis
* Percentage analysis
* Growth analysis
* Ranking

### Data Modeling

* Entity relationships
* One-to-many relationships
* Referential integrity
* Controlled categorical values

### Business Intelligence

* Preparing data for Power BI
* Designing analytical metrics
* Identifying dashboard KPIs
* Translating business questions into SQL queries

---

# 24. Conclusion

The **Financial Database & Revenue Analysis System** demonstrates how a
relational MySQL database can be designed and analyzed to answer
practical financial business questions.

The project combines:

```text
Database Design
      ↓
Data Modeling
      ↓
Data Storage
      ↓
SQL Analysis
      ↓
Business Metrics
      ↓
Decision Support
```

The most important analytical components include monthly revenue
analysis, top deposit customers, account balance analysis, transaction
activity, deposit-versus-withdrawal percentages, revenue growth,
revenue-source contribution, active-account analysis, customer
acquisition trends, and account balance analysis.

The project also demonstrates awareness of real-world data-quality
considerations such as correctly defining relationships between financial entities.

Overall, this project provides a strong foundation for demonstrating
**SQL, relational database design, financial data analysis, and business
intelligence skills**

---

## Author

**Abayim Princewill**

 Data Analyst | SQL | Power BI | Excel | Data
Visualization

### Core Skills

`SQL` `MySQL` `Power BI` `DAX` `Excel` `Data Cleaning` `Data Analysis`
`Dashboard Development` `Reporting`


Use this README as the documentation for the GitHub repository and the
SQL file as the executable database/analysis script.

