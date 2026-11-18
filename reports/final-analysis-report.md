# Operations and Supply Chain Performance Analysis

## Final Project Analysis Report

**Project Type:** Data Analytics / Business Intelligence  
**Tools:** Microsoft Excel, Power BI, DAX, GitHub  
**Dataset:** Supply Chain Orders Dataset  
**Author:** Eruvwu Stephen Ijerhe

---

## 1. Executive Summary

This project analyses operational and supply chain delivery performance using an order-level dataset containing 5,010 records. The objective was to assess delivery reliability across suppliers, locations, products and time, identify performance gaps, and translate the findings into actionable business recommendations.

The analysis involved data inspection, cleaning, transformation, classification, exploratory analysis, data modelling and dashboard development. Microsoft Excel was used for initial data preparation, while Power BI and DAX were used to build the analytical model, calculate performance indicators and develop an interactive dashboard.

Following data preparation, the dataset contained 5,000 unique orders, comprising 4,687 delivered orders and 313 orders classified as cancelled because they had no delivery date.

The analysis revealed an overall on-time delivery rate of **37.29%**, indicating that 62.71% of delivered orders arrived after their promised dates. Performance varied across suppliers, locations and product categories, highlighting areas that could benefit from further operational investigation.

The project demonstrates the application of data analytics techniques to a practical supply chain performance problem, from raw data preparation to business intelligence reporting.

## 2. Business Problem

Reliable delivery performance is essential to effective supply chain operations. Delayed deliveries can affect customer satisfaction, inventory availability, operational planning and business relationships.

However, without structured performance monitoring, it can be difficult for management to determine:

- Whether suppliers consistently meet promised delivery dates.
- Which locations experience relatively higher delivery delays.
- Which products and categories have weaker delivery performance.
- How delivery performance changes over time.
- Where operational improvement efforts should be prioritised.

This project addresses these questions by analysing historical order and delivery records and presenting the results through an interactive Power BI dashboard.

## 3. Project Objectives

The primary objectives were to:

1. Inspect and prepare the raw dataset for analysis.
2. Identify and address data-quality issues, including duplicate orders, inconsistent text entries and missing values.
3. Classify orders according to delivery status and timeliness.
4. Develop key performance indicators for measuring delivery performance.
5. Compare delivery performance across suppliers, locations, products and categories.
6. Examine monthly delivery performance trends.
7. Develop an interactive Power BI dashboard to communicate findings.
8. Provide evidence-based recommendations for improving supply chain performance.

## 4. Dataset Overview

The project used an Excel workbook initially titled `dataset_raw`, containing one worksheet and 5,010 order records.

The dataset included the following fields:

| Column | Description |
|---|---|
| Order_ID | Unique order identifier |
| Order_Date | Date the order was placed |
| Promised_Date | Expected delivery date |
| Delivery_Date | Actual delivery date |
| Supplier | Supplier responsible for the order |
| Product | Product ordered |
| Category | Product category |
| Quantity | Quantity ordered |
| Status | Recorded order status |
| Location | Delivery location |

The dataset covered five suppliers, seven products and five delivery locations.

The analysis focused primarily on delivery timeliness, supplier performance, location performance, product performance and monthly delivery trends.

## 5. Data Preparation and Cleaning

Data preparation was carried out in Microsoft Excel before importing the relevant worksheets into Power BI.

Rather than modifying the original dataset directly, I preserved the original worksheet and created additional versions to maintain a clear record of the preparation process.

### 5.1 Worksheet Organisation

The original worksheet was renamed `Original_Ver1`.

The following working versions were subsequently created:

| Worksheet | Purpose |
|---|---|
| Original_Ver1 | Preserved copy of the original dataset |
| Ver2 | Initial cleaning, duplicate removal and delivery classification |
| Ver3 | Date formatting and standardisation |
| Ver4-Late&OnTime | Delivered orders classified as On Time or Late |
| Ver5-Cancelled | Orders without delivery dates, classified as Cancelled |

This approach maintained traceability between the original data and the prepared datasets.

### 5.2 Duplicate Removal

The initial dataset contained 10 duplicate orders.

Duplicates were identified using `Order_ID` alone. Verification showed that the duplicate records had identical values across all columns.

The duplicate records were removed, reducing the dataset from 5,010 to 5,000 unique orders.

### 5.3 Text Standardisation

Some supplier names contained unnecessary leading or trailing spaces, while some location names used inconsistent lowercase formatting.

These inconsistencies were corrected to improve data consistency and ensure that grouping and aggregation in Power BI would not treat equivalent names as separate categories.

### 5.4 Date Formatting

The `Order_Date`, `Promised_Date` and `Delivery_Date` columns were formatted as dates to support accurate date comparisons and time-based analysis.

### 5.5 Delivery Classification

A new column, `Is Delivery On Time?`, was introduced to classify each order.

The classification logic was:

- **Cancelled:** No delivery date was recorded.
- **On Time:** Actual delivery date was on or before the promised date.
- **Late:** Actual delivery date was after the promised date.

The Excel formula used was:

```excel
=IF([@[Delivery_Date(Converted)]]=0,"Cancelled",IF([@[Delivery_Date(Converted)]]<=[@[Promised_Date(Converted)]],"On Time","Late"))
```

### 5.6 Dataset Segregation

After classification, the dataset was separated into two worksheets:

- `Ver4-Late&OnTime`: Contains delivered orders classified as On Time or Late.
- `Ver5-Cancelled`: Contains orders without recorded delivery dates.

Only these two prepared worksheets were imported into Power BI.

The delivered-orders worksheet was used as the primary analytical table for delivery performance calculations.

### 5.7 Data Preparation Summary

| Preparation Activity | Result |
|---|---:|
| Original records | 5,010 |
| Duplicate records removed | 10 |
| Unique orders after cleaning | 5,000 |
| Delivered orders | 4,687 |
| Orders classified as cancelled | 313 |
| Missing quantity records in original dataset | 15 |
| Missing quantity records in delivered dataset | 14 |

The missing quantity discrepancy between the original dataset and the delivered-orders worksheet was retained as a data-quality limitation requiring further reconciliation.

## 6. Analytical Approach and Power BI Development

After completing the Excel preparation, I imported the relevant worksheets into Power BI to develop the analytical model and dashboard.

### 6.1 Data Modelling

A dedicated Calendar table was created to support time-based analysis.

The Calendar table was marked as a date table and connected to the delivered-orders table through the `Delivery_Date` column using an active one-to-many relationship.

This enabled monthly delivery performance analysis based on actual delivery dates.

### 6.2 DAX Measures

DAX was used to create reusable measures for calculating key performance indicators.

The measures included:

- Total Delivered Orders
- On-Time Deliveries
- Late Deliveries
- On-Time Delivery Rate
- Late Delivery Rate
- Orders with Missing Quantity
- Orders with Recorded Quantity
- Missing Quantity Rate
- Average Delivery Lead Time

The `Average Delivery Lead Time` measure used `AVERAGEX` and `DATEDIFF` to calculate the average number of calendar days between order placement and delivery. It excluded records with missing dates and records where delivery occurred before the order date.

These measures enabled consistent calculations across the dashboard's different analytical views.

### 6.3 Dashboard Development

An interactive Power BI dashboard was developed to present the analysis through KPI cards, charts and comparative visualisations.

The dashboard covered:

1. Overall supply chain performance.
2. Supplier delivery performance.
3. Location delivery performance.
4. Product and category performance.
5. Monthly delivery performance trends.

The dashboard screenshots and Power BI report file are included in this GitHub repository.

## 7. Key Performance Indicators

The following indicators were calculated using the delivered-orders dataset.

| KPI | Result |
|---|---:|
| Total Delivered Orders | 4,687 |
| On-Time Deliveries | 1,748 |
| Late Deliveries | 2,939 |
| On-Time Delivery Rate | 37.29% |
| Late Delivery Rate | 62.71% |
| Orders with Missing Quantity | 14 |
| Missing Quantity Rate | 0.30% |

### Interpretation

The overall on-time delivery rate of 37.29% indicates that fewer than four in every ten delivered orders arrived on or before their promised dates.

Conversely, 62.71% of delivered orders were late.

This represents a significant delivery reliability gap and suggests that improving adherence to promised delivery dates should be a priority for further operational investigation.

## 8. Supplier Performance Analysis

Supplier performance was evaluated using delivered order volume, on-time delivery rate and late delivery count.

| Supplier | Delivered Orders | On-Time Rate | Late Deliveries |
|---|---:|---:|---:|
| NorthStar Supplies | 915 | 38.14% | 566 |
| Atlantic Wholesale | 981 | 37.72% | 611 |
| Prime Source Ltd | 944 | 37.61% | 589 |
| GreenLine Distribution | 943 | 37.01% | 594 |
| Calabar Trade Hub | 904 | 35.95% | 579 |

### Key Findings

- NorthStar Supplies recorded the highest on-time delivery rate at 38.14%.
- Calabar Trade Hub recorded the lowest rate at 35.95%.
- Atlantic Wholesale handled the highest number of delivered orders and recorded the highest late delivery count.
- The difference between the highest and lowest supplier on-time rates was 2.19 percentage points.

### Interpretation

Supplier delivery performance was relatively close across the five suppliers, with no supplier achieving an on-time rate above 40%.

The results suggest that delivery delays are not limited to a single supplier. Management may therefore need to examine both supplier-specific issues and broader supply chain processes.

Atlantic Wholesale's higher late delivery count should also be considered alongside its larger order volume rather than interpreted as evidence of poorer performance solely from the count.

## 9. Location Performance Analysis

Delivery performance was also compared across the five delivery locations.

| Location | Delivered Orders | On-Time Rate | Late Deliveries |
|---|---:|---:|---:|
| Uyo | 918 | 39.54% | 555 |
| Abuja | 966 | 39.03% | 589 |
| Lagos | 976 | 36.37% | 621 |
| Enugu | 914 | 36.21% | 583 |
| Calabar | 913 | 35.27% | 591 |

### Key Findings

- Uyo recorded the highest on-time delivery rate at 39.54%.
- Calabar recorded the lowest rate at 35.27%.
- Lagos had the highest delivered order volume and the highest late delivery count.
- The difference between Uyo and Calabar was 4.27 percentage points.

### Interpretation

Delivery performance varied across locations, with Uyo and Abuja performing relatively better than the other locations.

Calabar's lower on-time rate suggests that its delivery operations may require closer examination.

However, the available dataset does not provide enough information to establish whether the differences are caused by transportation, infrastructure, supplier allocation, distance or other operational factors.

## 10. Product and Category Performance

Product and category analysis was conducted to identify differences in delivery reliability across the items being supplied.

### 10.1 Category Performance

| Category | On-Time Rate | Late Deliveries |
|---|---:|---:|
| Networking | 34.33% | 417 |
| Furniture | 37.31% | 835 |
| Office Equipment | 37.62% | 441 |
| Consumables | 37.88% | 833 |
| Computers | 38.54% | 413 |

### 10.2 Individual Product Performance

| Product | On-Time Rate | Late Deliveries |
|---|---:|---:|
| Router | 34.33% | 417 |
| Chair | 34.91% | 414 |
| Desk | 39.51% | 421 |
| Printer | 37.62% | 441 |
| Ink | 37.50% | 405 |
| Paper | 38.24% | 428 |
| Laptop | 38.54% | 413 |

### Key Findings

- Networking recorded the lowest category on-time delivery rate at 34.33%.
- Computers recorded the highest category rate at 38.54%.
- Router was the weakest-performing individual product by on-time delivery rate.
- Desk recorded the highest individual product on-time rate at 39.51%.
- Furniture and Consumables together accounted for 1,668 late deliveries, approximately 56.8% of all late deliveries.

### Interpretation

The results reveal differences in delivery performance across product categories and individual products.

Networking products, particularly routers, may warrant further investigation to determine whether sourcing, supplier allocation or fulfilment processes contribute to their weaker performance.

Furniture and Consumables also represent a substantial share of late deliveries, making them relevant areas for improvement initiatives.

These findings identify areas for investigation but do not establish the underlying causes of delays.

## 11. Monthly Delivery Performance Trends

Monthly delivery performance was analysed using the Calendar table and the active relationship with Delivery_Date.

The analysis focused on the monthly On-Time Delivery Rate to identify changes in delivery reliability over time.

### Key Observations

Delivery performance fluctuated across the months rather than following a consistent upward or downward pattern.

Some months recorded relatively stronger delivery performance, while others experienced noticeable declines.

The available 2026 records cover January to July only, so the year should not be compared with a complete 2025 reporting period without accounting for the difference in coverage.

### Interpretation

The monthly analysis provides a basis for monitoring delivery reliability and identifying periods that may require further investigation.

A more detailed time-series analysis, supported by additional operational information, could help determine whether the observed fluctuations are associated with seasonal demand, supplier capacity, transportation constraints or other factors.

## 12. Key Business Insights

The analysis produced several important findings:

1. Delivery reliability is a major performance concern.

With an on-time delivery rate of 37.29%, the dataset indicates that late deliveries represent a substantial proportion of completed orders.

2. Supplier performance is relatively consistent but weak overall.

The supplier on-time delivery rates range from 35.95% to 38.14%. This suggests that improvement efforts should not focus exclusively on one supplier.

3. Delivery performance differs by location.

Uyo recorded the strongest on-time performance, while Calabar recorded the weakest. Further investigation could help identify location-specific operational constraints.

4. Product categories contribute differently to late deliveries.

Networking had the lowest on-time rate, while Furniture and Consumables accounted for a considerable share of late delivery volume.

5. Monthly performance is inconsistent.

The fluctuations in monthly delivery rates highlight the importance of continuous performance monitoring rather than relying only on aggregate results.

6. Data quality remains an important consideration.

Missing quantity records and orders without delivery dates demonstrate the importance of accurate and complete operational data when measuring supply chain performance.

## 13. Recommendations

Based on the findings, the following actions are recommended:

### 13.1 Strengthen Supplier Performance Monitoring

Introduce regular supplier performance reviews using on-time delivery rate, late delivery volume and order volume.

Supplier improvement discussions should be supported by delivery records and agreed performance targets.

### 13.2 Investigate Location-Specific Delivery Challenges

Conduct further operational reviews in locations with lower on-time delivery performance, particularly Calabar.

The review should examine transportation arrangements, delivery routes, supplier allocation and other relevant operational factors.

### 13.3 Prioritise Underperforming Products and Categories

Investigate the delivery processes associated with Networking products, particularly routers.

Also examine the high late delivery volumes associated with Furniture and Consumables to determine where process improvements could have the greatest impact.

### 13.4 Improve Delivery Planning and Monitoring

Strengthen order tracking and establish early-warning mechanisms for orders approaching their promised delivery dates.

This could help operations teams identify potential delays before delivery deadlines are missed.

### 13.5 Improve Data Quality and Record-Keeping

Establish data validation procedures to reduce missing quantity values, incomplete delivery records and inconsistent supplier or location entries.

Orders without delivery dates should also be reviewed to confirm whether they were genuinely cancelled, remain pending or fall into another status category.

### 13.6 Establish Continuous Performance Reporting

Use the Power BI dashboard as a foundation for regular supply chain performance reviews.

Monitoring delivery indicators over time can help management assess progress, identify emerging issues and evaluate the effectiveness of improvement initiatives.

## 14. Project Limitations

The analysis was subject to the following limitations:

Quantity measurement: The Quantity field represents the number of items ordered, not the quantity actually delivered. Therefore, the analysis cannot determine whether orders were fulfilled completely or partially.

Missing quantity values: The original dataset contained 15 records with missing quantity values, while the delivered-orders dataset contained 14. This discrepancy requires further reconciliation.

Orders without delivery dates: A total of 313 orders had no recorded delivery date and were classified as Cancelled for this analysis. Their actual operational status could not be independently verified.

Limited operational context: The dataset did not contain information about transportation costs, delivery routes, warehouse capacity, inventory availability or reasons for delays.

Incomplete 2026 coverage: The available 2026 records covered January to July only.

No causal analysis: The available variables support performance comparisons but are insufficient to establish the causes of delivery delays.

These limitations should be considered when interpreting the results and making operational decisions.

## 15. Future Improvements

Future development of the project could include:

Incorporating actual delivered quantities to measure order fulfilment rates.

Adding transportation and logistics cost data.

Analysing supplier lead times and delivery consistency.

Investigating the relationship between order volume and delivery performance.

Introducing delivery delay duration analysis.

Developing supplier and location performance scorecards.

Adding target-based KPI monitoring and alerts.

Incorporating additional periods of data for more comprehensive trend analysis.

Using predictive analytics to identify orders at risk of late delivery.

## 16. Conclusion

This project demonstrates how data analytics and business intelligence tools can be applied to examine supply chain delivery performance.

Through structured data preparation in Excel, analytical modelling in Power BI, DAX measure development and interactive dashboard design, I transformed a raw order dataset into a set of performance indicators and business insights.

The analysis identified a low overall on-time delivery rate, variations in supplier and location performance, differences across product categories and fluctuations in monthly delivery performance.

Beyond the dashboard itself, the project demonstrates my ability to approach a business problem systematically, prepare and validate data, develop analytical measures, interpret results and communicate evidence-based recommendations.

It also highlights the importance of data quality, appropriate KPI selection and understanding analytical limitations when supporting operational decision-making.

## 17. Project Resources

GitHub Repository: Operations and Supply Chain Performance Analysis

Power BI Dashboard: Available in the repository's dashboard folder.

Dashboard Screenshots: Available in the repository's screenshots folder.

DAX Measures: Available in dax/measures.md.

## 18. Author

Eruvwu Stephen Ijerhe

Operations and Supply Chain Professional | Data Analytics | Business Intelligence | Project Management

GitHub: github.com/sterijaz
