# Customer Support Performance Analysis in Excel

## Project Overview

This project analyzes a customer-support dataset using Microsoft Excel to demonstrate how raw operational data can be cleaned, structured, analyzed, and transformed into practical business insights.

The project focuses on customer inquiries, support activity, interaction patterns, time-of-day activity, and data-quality considerations that may affect reporting.

Rather than focusing only on applying Excel formulas, the analysis uses those formulas to answer practical business questions and develop measurable KPIs.

## Business Question

**How effectively are customer-support teams responding to customer interactions, and what patterns could help improve support performance?**

## Project Workflow

**Raw Data → Data Cleaning → Analysis → KPIs → Business Insights**

## Dataset

The project uses a customer-support dataset containing Twitter-based customer service interactions.

The raw dataset includes:

- Tweet IDs
- Author IDs
- Inbound/outbound interaction status
- Interaction timestamps
- Message content
- Response tweet relationships

The original raw data has been preserved in the workbook so that the cleaning and transformation process can be reviewed against the source data.

## Data Cleaning & Preparation

The raw dataset was prepared for analysis using Microsoft Excel.

### Tweet ID

Tweet IDs were standardized using `TRIM` to remove unnecessary spaces and ensure consistency.

Tweet IDs were treated as identifiers rather than numerical values.

### Author ID

Author IDs were also standardized using `TRIM`.

The column contains both numeric identifiers and support account names, so the values were treated as identifiers rather than numerical measures.

### Message Direction

The original inbound/outbound values were TRUE/FALSE values.

An `IF` formula was used to convert these into more meaningful categories:

- `TRUE` → Customer
- `FALSE` → Support
- Other values → Check

This created a clearer **Message Direction** field for analysis.

### Interaction Date

The original `created_at` field contained timestamps in text format.

A combination of `DATE`, `MATCH`, `MID`, and `RIGHT` was used to extract the:

- Day
- Month
- Year

and convert the text into a usable Excel date.

### Interaction Time

The time component was extracted from the original timestamp using `TIMEVALUE` and `MID`.

This created a separate **Interaction Time** field that could be used for time-based analysis.

### Time of Day

Interactions were grouped into four time periods:

| Time Period | Time Range |
|---|---|
| Overnight | 00:00:00–05:59:59 |
| Morning | 06:00:00–11:59:59 |
| Afternoon | 12:00:00–17:59:59 |
| Evening | 18:00:00–23:59:59 |

An `IF` formula was used to categorize each interaction according to its time.

### Message Content

The original message content was retained as provided in the source dataset.

Some messages contain HTML entities such as `&amp;` and `&gt;`, as well as encoding issues affecting some characters and emojis.

Rather than making potentially unreliable corrections, these issues were treated as data-quality considerations for reporting.

### Response Relationship Fields

The dataset contains `Response Tweet ID` and `Response Relationship` fields that can help identify relationships between customer inquiries and support responses.

However, some response IDs appear incomplete, blank, or combined. Because of this, the fields were treated cautiously and were not used to make unsupported assumptions about whether every customer inquiry received a response.

## Analysis

The analysis was designed around practical customer-support questions rather than simply demonstrating Excel formulas.

### Question 1: How many customer inquiries and support responses are in the dataset?

`COUNTA` was used to calculate the total number of interactions.

`COUNTIF` was then used to separate customer inquiries from support responses based on the **Message Direction** column.

The analysis identified:

- **93 total interactions**
- **49 customer inquiries**
- **44 support responses**
- **53% customer activity**
- **47% support activity**

These figures provide an overview of customer activity and support activity within the dataset.

The response relationship fields were also considered when assessing how interactions may be connected. However, because some response IDs appear incomplete or combined, the number of support responses cannot automatically be treated as the number of inquiries successfully answered.

### Question 2: Are customer inquiries and support activity concentrated during the same parts of the day?

`COUNTIFS` was used to count customer inquiries and support responses within each time-of-day period.

Percentage calculations were then used to determine the share of total customer activity and support activity represented by each period.

An **Activity Gap** was calculated by comparing Customer Activity % with Support Activity %.

This helps identify periods where customer activity and support activity are more or less aligned.

An activity gap does not automatically mean that customers experienced slow or poor service because response time was not calculated in this analysis.

## Key Performance Indicators

The project developed the following KPIs:

- Total Interactions
- Customer Inquiries
- Support Responses
- Customer Activity %
- Support Activity %
- Customer Activity by Time of Day
- Support Activity by Time of Day
- Activity Gap

## Key Results

### Overall Interaction Activity

| KPI | Result |
|---|---:|
| Total Interactions | 93 |
| Customer Inquiries | 49 |
| Support Responses | 44 |
| Customer Activity | 53% |
| Support Activity | 47% |

Customer inquiries slightly exceeded support responses, with 49 inquiries compared with 44 support responses.

While this is not a large difference, it highlights the importance of monitoring support coverage and understanding how customer inquiries connect to recorded support responses.

### Time-of-Day Analysis

| Time of Day | Customer Inquiries | Customer % | Support Responses | Support % | Total Interactions |
|---|---:|---:|---:|---:|---:|
| Overnight | 3 | 6% | 2 | 5% | 5 |
| Morning | 14 | 29% | 2 | 5% | 16 |
| Afternoon | 31 | 63% | 40 | 91% | 71 |
| Evening | 1 | 2% | 0 | 0% | 1 |
| **Total** | **49** | **100%** | **44** | **100%** | **93** |

## Business Insights

### 1. Customer inquiries slightly exceeded support responses

The dataset contains 49 customer inquiries compared with 44 support responses.

Although the difference is relatively small, it suggests that some customer inquiries may not have a corresponding recorded support response.

However, this should not be interpreted as a confirmed response gap because the response relationship fields contain incomplete or combined values in some cases.

### 2. Most customer activity occurred in the afternoon

The afternoon accounted for **63% of customer inquiries**.

Support activity was even more concentrated during the afternoon, accounting for **91% of support activity**.

This indicates that the afternoon was the most active period for both customers and support teams.

### 3. Morning showed the largest activity gap

Morning represented **29% of customer inquiries**, compared with only **5% of support activity**.

This represents a **24 percentage-point activity gap**.

The gap indicates that customer activity and support activity were less aligned during the morning.

It does not establish that customers experienced slow responses because actual response time was not calculated.

### 4. Evening activity was minimal

Only **2% of customer inquiries** and **0% of support activity** occurred during the evening.

This suggests that the dataset contains very limited evening activity, so conclusions about evening support performance should be treated cautiously.

## Recommendation

Support teams could monitor inquiry volumes throughout the day and review support coverage during periods where customer activity and support activity are less aligned.

The analysis suggests that morning activity may be worth monitoring because customer inquiries represented a larger share of activity than support responses during this period.

A broader objective would be to move closer to complete response coverage for identifiable customer inquiries, provided that the underlying response relationship data is sufficiently reliable to measure this accurately.

## Data Quality Considerations

Data quality is an important part of this analysis because the reliability of business insights depends on the quality of the underlying data.

The project identified several considerations:

- Some response relationship fields are blank.
- Some response IDs appear combined or incomplete.
- Message content contains HTML entities and encoding issues.
- The original timestamps were stored as text rather than Excel date/time values.
- Author IDs contain both numeric identifiers and support account names.

These issues were documented rather than making assumptions that could introduce inaccuracies into the analysis.

## Excel Skills & Techniques Applied

### Data Cleaning & Preparation

- Data cleaning
- Data preparation
- Data structuring
- Identifier standardization
- Text-to-date conversion
- Text-to-time conversion
- Data consistency checks
- Data-quality assessment
- Preserving raw source data

### Excel Functions

The project applied:

- `TRIM`
- `IF`
- `COUNTA`
- `COUNTIF`
- `COUNTIFS`
- `DATE`
- `TIME`
- `TIMEVALUE`
- `MATCH`
- `MID`
- `RIGHT`

### Data Analysis

- Percentage calculations
- Customer vs. support activity analysis
- Time-of-day categorization
- Activity-gap analysis
- KPI development
- Data-quality assessment
- Business insight generation

## Project Outcome

This project demonstrates how Microsoft Excel can be used to move from raw operational data to structured analysis and business-focused insights.

It demonstrates practical experience in:

**Data Cleaning → Data Analysis → KPI Development → Business Insights**

The project also highlights an important aspect of data analysis: recognizing when the available data has limitations and avoiding conclusions that the data cannot reliably support.

## Tools Used

- Microsoft Excel
- GitHub

## Project Structure

```text
customer-support-performance-analysis-excel/
│
├── Customer Support Performance Analysis.xlsx
├── README.md
└── screenshots/
    ├── cleaned-data.png
    ├── support-analysis.png
    └── time-of-day-analysis.png
