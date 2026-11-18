# DAX Measures Documentation

## Operations and Supply Chain Performance Analysis

This document contains the DAX measures developed for the Operations and Supply Chain Performance Analysis Dashboard using Microsoft Power BI.

The measures evaluate delivery performance, monitor data completeness and analyse delivery lead times.

### 1. Total Delivered Orders

```dax
Total Delivered Orders =
COUNTROWS('Ver4-Late&OnTime')
```

**Purpose:** Counts all records in the delivered-orders table.

**Result:** 4,687 delivered orders.

### 2. On-Time Deliveries

```dax
On-Time Deliveries =
CALCULATE(
    COUNTROWS('Ver4-Late&OnTime'),
    'Ver4-Late&OnTime'[Is Delivery On Time?] = "On Time"
)
```

**Purpose:** Counts orders delivered on or before their promised delivery dates.

**Result:** 1,748 orders.

### 3. Late Deliveries

```dax
Late Deliveries =
CALCULATE(
    COUNTROWS('Ver4-Late&OnTime'),
    'Ver4-Late&OnTime'[Is Delivery On Time?] = "Late"
)
```

**Purpose:** Counts orders delivered after their promised delivery dates.

**Result:** 2,939 orders.

### 4. On-Time Delivery Rate

```dax
On-Time Delivery Rate =
DIVIDE(
    [On-Time Deliveries],
    [Total Delivered Orders],
    0
)
```

**Purpose:** Calculates the percentage of delivered orders completed on or before their promised dates.

**Result:** 37.29%.

### 5. Late Delivery Rate

```dax
Late Delivery Rate =
DIVIDE(
    [Late Deliveries],
    [Total Delivered Orders],
    0
)
```

**Purpose:** Calculates the percentage of delivered orders completed after their promised dates.

**Result:** 62.71%.

### 6. Orders with Missing Quantity

```dax
Orders with Missing Quantity =
CALCULATE(
    COUNTROWS('Ver4-Late&OnTime'),
    ISBLANK('Ver4-Late&OnTime'[Quantity])
)
```

**Purpose:** Counts delivered orders with missing quantity information.

**Result:** 14 orders.

### 7. Orders with Recorded Quantity

```dax
Orders with Recorded Quantity =
CALCULATE(
    COUNTROWS('Ver4-Late&OnTime'),
    NOT ISBLANK('Ver4-Late&OnTime'[Quantity])
)
```

**Purpose:** Counts delivered orders with recorded quantity values.

### 8. Missing Quantity Rate

```dax
Missing Quantity Rate =
DIVIDE(
    [Orders with Missing Quantity],
    [Total Delivered Orders],
    0
)
```

**Purpose:** Calculates the percentage of delivered orders with missing quantity information.

**Result:** 0.30%.

### 9. Average Delivery Lead Time

```dax
Average Delivery Lead Time =
AVERAGEX(
    FILTER(
        'Ver4-Late&OnTime',
        NOT ISBLANK('Ver4-Late&OnTime'[Order_Date]) &&
        NOT ISBLANK('Ver4-Late&OnTime'[Delivery_Date]) &&
        'Ver4-Late&OnTime'[Delivery_Date] >= 'Ver4-Late&OnTime'[Order_Date]
    ),
    DATEDIFF(
        'Ver4-Late&OnTime'[Order_Date],
        'Ver4-Late&OnTime'[Delivery_Date],
        DAY
    )
)
```

**Purpose:** Calculates the average number of calendar days between order placement and actual delivery.

The calculation excludes records with missing dates and records where the delivery date precedes the order date.

### 10. Data Model and Calculation Notes

- `'Ver4-Late&OnTime'` represents the delivered-orders dataset imported from the Excel worksheet of the same name.
- Cancelled orders were stored separately and excluded from the main delivered-order calculations.
- Each row represents one delivered order.
- The Calendar table is connected to the delivered-orders table through `Delivery_Date`.
- Delivery performance rates use delivered orders as the denominator.
- Percentage measures should be formatted as percentages in Power BI.
- Average Delivery Lead Time returns a value in days.

### Conclusion

These DAX measures provide the foundation for monitoring delivery performance, comparing suppliers and locations, evaluating product performance, and identifying data-quality issues within the supply chain.
