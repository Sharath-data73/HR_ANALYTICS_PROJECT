# HR-Analytics-Project
## Overview: Employee Attendance Analysis for AtliQ Technologies
## Problem Statement:
The HR department at AtliQ Hardware faced significant challenges in monitoring and managing employee attendance. Specifically, they needed a clear picture of employee preferences for working from home (WFH) versus the office, along with insights into the reasons behind these choices. Moreover, tracking sick leaves and understanding how often employees take leave were essential to improving workforce management and planning

The problem was Escalated by the fact that data was scattered across multiple Excel sheets, each representing different months and containing daily attendance data. To enable data-driven decision-making, the HR team required a centralized solution to gather, transform, and analyze this data efficiently.
## Key Challenges and Solutions:

### 1. Data Spread Across Different Excel Files
Challenge: The attendance data was split across several Excel files—one for each month. Each file had daily attendance as separate columns, making it hard to bring everything together.
Solution: I used Power Query to merge all the monthly files into one complete dataset with consistent formatting.

### 2. Restructuring Data for Better Analysis
Challenge: Every file had a separate column for each day, which made time-based analysis difficult.
Solution: I transformed the data using Power Query to convert multiple date columns into a single "Date" column, enabling proper time-series analysis.

### 3. Handling Complex Data Cleanup
Challenge: HR needed clear and useful insights from the data, which required a deeper level of processing.
Solution: I used advanced Power Query features like pivoting, parameter handling, and custom functions to automate and streamline the data cleaning process.

#### Data Preparation with Power Query
The original attendance files contained monthly records with columns for different attendance types like "Present," "Work From Home," "Sick Leave," and "Other Leave." Using Power Query, I reshaped this data into a format that's easier to analyze and visualize.

## Key Steps:

### Combining Multiple Excel Sheets:

Using Power Query's Append Queries feature, I merged multiple workbooks into one comprehensive dataset.
Consolidating Date Columns:

I transformed the daily columns into a single Date column using Unpivot Columns, creating a normalized structure that allowed further time-based analysis.
Handling Data Inconsistencies:

I ensured consistent formatting across datasets, cleaning errors and removing duplicates.
Automating Data Refresh:

Built a dynamic refresh mechanism in Power Query that allows easy updates as new monthly data is added, ensuring the system remains scalable.

## Metrics Creation using DAX:
Once the data was cleaned and consolidated, I built custom metrics using DAX (Data Analysis Expressions) to generate insights relevant to the HR team.

## Key Metrics:
- Employee Attendance Trend: Tracks daily and monthly presence trends across the workforce.
- Sick Leave Percentage: Measures the proportion of employees on sick leave for any given period.
- Work From Home (WFH) Analysis: Calculates WFH patterns and highlights preferences over time.
- Leave Analysis: Insights into the frequency and reasons for leave, broken down by department or team.

## DAX formulas:
-presence% = DIVIDE([present days],[totalworkingdays],0)

-present days = 
var presentdays=CALCULATE(count('Final Data'[Value]),'Final Data'[Value]="p")
return
presentdays+[WFH COUNT1]

-SL % = DIVIDE([SL COUNT1],[totalworkingdays],0)

-SL COUNT1 = SUM('Final Data'[SL COUNT])

-totalworkingdays = 
var totaldays = COUNT('Final Data'[Value])
var nonworkingdays = CALCULATE(COUNT('Final Data'[Value]),'Final Data'[Value] in {"WO","HO"})
RETURN
totaldays-nonworkingdays

-WFH % = DIVIDE([WFH COUNT1],[present days],0)

-WFH COUNT1 = SUM('Final Data'[WFH COUNT])

-day of week = FORMAT('Final Data'[Date],"ddd")

-month = STARTOFMONTH('Final Data'[Date])

-SL COUNT = SWITCH(TRUE(),'Final Data'[Value] = "SL",1,'Final Data'[Value] ="HSL",0.5,0)

-WFH COUNT = SWITCH(TRUE(),'Final Data'[Value] = "WFH",1,'Final Data'[Value] ="HWFH",0.5,0)

## Key Insights:
The final dashboard provided actionable insights, including:

- Employee Attendance Heatmap: Visualized trends in employee presence across departments and months.
- WFH Trends: Highlighted a shift toward remote work preferences, which helped HR make decisions about flexible work arrangements.
- Sick Leave Patterns: Detected spikes in sick leaves, providing HR with data to potentially address wellness programs or adjust policies.
- Leave Frequency: Identified departments with higher leave rates, helping HR focus on engagement strategies.

| HR Employee Insights |
| ----------- |
![My Image](![DASHBOARD IMAGE](https://github.com/user-attachments/assets/b132b171-97c7-4df8-8e8c-fac1aa3b2f48)
)

  
## Tools, Software, and Techniques:
- Microsoft Excel: Source data stored across multiple Excel workbooks.
- Power Query: Used for data cleaning, transformation, and combining multiple sheets into a single dataset.
- Power BI: Visualization and dashboard creation using DAX to develop key metrics.
- DAX (Data Analysis Expressions): Used for creating custom metrics and calculations.

# References:
- Power Query Documentation: https://learn.microsoft.com/en-us/power-query/
- DAX Guide: https://dax.guide/









