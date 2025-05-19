# Real-Time Data Ingestion with Eventstream in Microsoft Fabric

## Overview
This lab demonstrates how to use Microsoft Fabric's Eventstream feature to capture, transform, and route real-time bicycle sharing system data to an Eventhouse for analysis.

## Prerequisites
- Microsoft Fabric tenant
- Web browser access

## Lab Steps

### 1. Setup Environment
1. Create a new Fabric workspace with capacity
2. Create an Eventhouse resource with KQL database

### 2. Configure Eventstream Pipeline
1. **Create Eventstream**:
   - Name: `Bicycle-data`
   - Use sample bicycle sharing data source

2. **Add Destination**:
   - Configure Eventhouse destination
   - Create `bikes` table for raw data

### 3. Data Transformation
1. Add **Group By** transformation:
   - Aggregate bicycles by street
   - 5-second tumbling windows
   - Output to `bikes-by-street` table

2. Publish transformations

### 4. Query Data
```kql

// Raw data

bikes

| where ingestion_time() between (now(-1d) .. now())

// Transformed data

['bikes-by-street']

| summarize TotalBikes = sum(tolong(SUM_No_Bikes))
 
  by Window_End_Time, Street

| sort by Window_End_Time desc, Street asc
```

## Key Learnings
- Real-time data ingestion with Eventstream
- Windowing and aggregation transformations
- KQL database configuration in Eventhouse
- Time-series data analysis techniques

## Clean Up
1. Navigate to workspace settings
2. Select "Remove this workspace"

### 👤 Author >> Sefa Öztürk
IT Trainee | Azure Data Engineer in progress

📇 LinkedIn: https://www.linkedin.com/in/sefa-ozturk1972
