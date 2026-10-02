# Hotel Booking Data Engineering & Analytics

An end-to-end data engineering and analytics project that transforms raw hotel booking data into a structured data warehouse and business insights through an ETL pipeline.

**Project Type:** Data Engineering & Business Analytics
**Focus:** ETL · Data Warehouse · Data Analysis
**Tools:** Pentaho Data Integration · MySQL · Power BI

---

## Project Overview

Hotel booking data contains valuable information about reservations, customer behaviour, cancellations, revenue, and booking channels. However, raw operational data requires proper cleaning, transformation, and structuring before it can be reliably used for business analysis.

This project focuses on building an **ETL pipeline using Pentaho Data Integration** to transform raw hotel booking data into an analysis-ready **MySQL data warehouse**, which is then connected to Power BI for business analysis and visualization.

The overall workflow is:

**Raw CSV → Pentaho ETL → Data Cleaning & Transformation → MySQL Data Warehouse → Business Analysis → Power BI**

The main emphasis of this project is the **ETL process and data warehouse design**, while Power BI serves as the final analytical layer.

---

## Business Context

The project aims to transform hotel booking data into a structured analytical environment that can be used to explore:

* Booking and cancellation patterns
* Revenue performance
* Seasonal demand
* Customer and market segments
* Distribution channels
* Hotel booking behaviour

The resulting data warehouse provides a structured foundation for business intelligence and data-driven analysis.

---

## Dataset

The project uses the **Hotel Booking Demand** dataset from Kaggle.

The dataset contains:

* **119,390 reservation records**
* **36 attributes**
* City Hotel and Resort Hotel bookings
* Booking data from **July 2015 to August 2017**

The dataset includes information such as:

* Hotel type
* Booking dates
* Length of stay
* Customer type
* Market segment
* Distribution channel
* Deposit type
* Room type
* Country
* Average Daily Rate (ADR)
* Booking status

The dataset is used as the primary source for the ETL pipeline.

---

## ETL Pipeline

### 1. Extract — Load Raw Data

The raw CSV dataset is imported into a MySQL staging environment using **Pentaho Data Integration**.

The initial transformation consists of:

**CSV File Input → Select Values → Table Output**

The imported records are stored in the `raw_booking` table.

The staging layer provides a consistent starting point for the subsequent ETL processes while keeping the raw data separate from processed data.

---

### 2. Transform — Data Cleaning

The raw data is cleaned and validated before being loaded into the analytical warehouse.

The cleaning process includes:

* Data type standardization
* Handling missing values
* Removing highly incomplete attributes
* Filtering invalid records
* Removing duplicates
* Preparing analysis-ready attributes

Specific transformations include:

* Removing the `company` attribute because of its high proportion of NULL values
* Replacing NULL `agent` values with `0`
* Filtering records where `adults <= 0`
* Filtering records where `average_daily_rate < 0`
* Filtering records where `stays_in_week_nights <= 0`
* Filtering records where `stays_in_weekend_nights <= 0`

The cleaned data is stored in the `processed_booking` table.

---

### 3. Transform — Feature Engineering

The ETL pipeline generates additional attributes to support business analysis.

#### Total Nights

```text
total_nights =
stays_in_week_nights + stays_in_weekend_nights
```

#### Estimated Revenue

```text
estimated_revenue =
average_daily_rate × total_nights
```

#### Season Classification

Arrival months are transformed into three seasonal categories:

* **High Season:** December, January, February
* **Peak Summer:** June, July, August
* **Regular Season:** Remaining months

These transformations convert raw operational attributes into analytical features that can be used for further analysis.

---

## Data Warehouse

The processed data is organized into a **MySQL star-schema data warehouse**.

The warehouse consists of:

**1 Fact Table + 11 Dimension Tables**

### Fact Table

**`fact_booking`**

The fact table contains booking transaction records and connects each booking to the relevant dimensions using surrogate keys.

### Dimension Tables

The warehouse contains dimensions for:

* Hotel
* Date
* Guest
* Meal
* Country
* Market Segment
* Distribution
* Room Type
* Deposit Type
* Agent
* Customer Type

The star schema separates transactional information from descriptive attributes and provides a structured foundation for multidimensional analysis.

---

## Slowly Changing Dimensions

Different Slowly Changing Dimension strategies were applied according to the characteristics of each dimension.

### SCD Type 2 — Guest

The Guest Dimension uses **Slowly Changing Dimension Type 2** to preserve historical changes in guest information.

When relevant guest attributes change, a new record is created instead of overwriting the existing record.

### SCD Type 0

SCD Type 0 was applied to relatively static dimensions, including:

* Date
* Distribution
* Room Type

This approach avoids unnecessary historical versioning for attributes that do not require change tracking.

---

## ETL Orchestration

The individual Pentaho transformations are organized into an ETL Job to control the execution sequence.

**Load Raw Data → Data Cleansing → Dimension Transformations → Fact Booking Load**

The order is important because dimension tables need to be populated before the fact table can resolve their surrogate keys.

The orchestration also reduces manual execution and helps ensure that transformations are processed in the intended order.

---

## Business Analysis

After the ETL process and warehouse loading were completed, the resulting data was connected to Power BI for business analysis.

The dashboard focuses on:

### Cancellation Analysis

Exploring cancellation behaviour based on booking conditions such as:

* Lead time
* Deposit type
* Previous cancellation behaviour

### Revenue & Seasonality

Analyzing revenue patterns across:

* Hotel type
* Month
* Season
* Average Daily Rate

### Market Segment

Comparing booking behaviour and performance across different market segments.

### Distribution Channel

Analyzing booking volume and cancellation patterns across distribution channels.

---

## Key Insights

### Cancellation Behaviour

The dashboard analysis reported a **39% cancellation rate**. Cancellation patterns varied based on booking conditions, particularly lead time and deposit type.

### Seasonality

Booking and revenue patterns varied across seasons, with stronger demand observed during the summer period, particularly July and August.

### Market Segment

Different market segments demonstrated different booking volumes and cancellation patterns, providing a basis for understanding customer acquisition channels.

### Distribution Channel

Distribution channels contributed differently to booking volume and booking behaviour, highlighting the importance of channel-level analysis.

---

## Dashboard

The processed warehouse data is visualized through an interactive **Power BI dashboard**.

### Dashboard Preview

![Power BI Dashboard](dashboard-preview/powerbi-dashboard.png)

The dashboard provides an analytical view of:

* Booking trends
* Cancellation patterns
* Revenue
* Seasonality
* Market segments
* Distribution channels
* Customer characteristics

**Power BI Report:**
[View Interactive Dashboard](YOUR_POWER_BI_LINK)

---

## Project Materials

### ETL

The `etl/` folder contains the main Data Engineering artifacts, including the **Pentaho ETL pipeline workflow** and **star schema/data warehouse design**.

### Data

The `data/` folder contains the dataset used as the source for the ETL pipeline.

### Dashboard Preview

The `dashboard-preview/` folder contains a preview of the final Power BI dashboard.

### Pitch Deck

The `pitchdeck/` folder contains the project presentation/report covering the **ETL process, data warehouse design, analytical findings, and business insights**.

---

## Tools & Technologies

| Area           | Technology               |
| -------------- | ------------------------ |
| ETL            | Pentaho Data Integration |
| Database       | MySQL                    |
| Data Warehouse | Star Schema              |
| Visualization  | Power BI                 |
| Source Data    | CSV                      |
| Dataset        | Hotel Booking Demand     |

---

## Project Outcome

This project demonstrates an end-to-end data engineering workflow:

**Raw Data → ETL → Data Warehouse → Analysis → Visualization**

The ETL pipeline transforms raw hotel booking data through data cleaning, validation, transformation, feature generation, dimensional modelling, and fact table loading.

The resulting MySQL data warehouse provides a structured foundation for analyzing booking behaviour, cancellations, revenue, seasonality, market segments, and distribution channels.

---

## Portfolio

This project is part of my Data Engineering, Business Intelligence, and Data Analytics portfolio.

**Portfolio:** [Add Portfolio URL]

**Power BI Dashboard:** [View Dashboard](YOUR_POWER_BI_LINK)
