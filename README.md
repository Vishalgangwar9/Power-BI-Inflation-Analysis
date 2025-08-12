# Power-BI-Inflation-Analysis
This project involves creating an interactive Power BI dashboard by collecting, cleaning, and visualizing data to answer key business questions, providing actionable insights with scope for future enhancements.
1. Introduction Phase  
1.1 Project Introduction  
This project involves developing an interactive Power BI dashboard to visualize and analyze data effectively. It includes collecting, preparing, and visualizing data to create meaningful insights for decision-makers.
1.2 Objective  
The objective is to convert raw data into a structured and interactive dashboard that supports business decisions. This includes:
•	Connecting data sources
•	Data cleaning & transformation
•	Creating insightful visualizations
•	Designing a user-friendly dashboard
2. Project Initialization and Planning Phase  
2.1 Define Problem Statement  
There is a large amount of unorganized data that is hard to interpret manually. A centralized dashboard is required to convert this raw data into actionable insights.
2.2 Project Proposal  
The proposal outlines the aim to build a Power BI dashboard by:
•	Importing datasets
•	Creating relationships between tables
•	Designing visuals like bar charts, pie charts, and KPIs
2.3 Initial Project Planning  
Initial planning involved:
•	Identifying the source dataset
•	Defining project milestones
•	Allocating tasks (data cleaning, transformation, visual design, documentation)
3. Technical Architecture and Project Flow  
1) Data Collection - Gathering and connecting the dataset with Power BI.
2) Data Preparation - Cleaning and transforming the data for visualization.
3) Data Visualizations - Building charts and graphs to represent data.
4) Dashboard - Designing a responsive and interactive dashboard.
5) Report - Creating a well-structured report with insights.
6) Performance Testing - Optimizing filters, calculations, and visuals.
7) Project Demonstration and Documentation - Recording explanation and preparing documentation.

formula use 
Adjustedinflationrate

Adjustedinflationrate = global_inflation_data[Inflationrate]*.01

InflationRateCategory
InflationRateCategory = 
switch(
    True(),
    'global_inflation_data'[Inflationrate]< 2,"Low Inflation",
    'global_inflation_data'[Inflationrate] < 5, "moderate Inflation","high"
)
InflationRateChange
InflationRateChange = 
VAR CurrentYear = VALUE(MAX('global_inflation_data'[Year]))
VAR CurrentInflationRate =
    CALCULATE(
        MAXX('global_inflation_data', VALUE('global_inflation_data'[Inflationrate])),
        FILTER(
            ALL('global_inflation_data'),
            VALUE('global_inflation_data'[Year]) = CurrentYear
        )
    )
VAR PreviousInflationRate = 
    CALCULATE(
        MAXX('global_inflation_data', VALUE('global_inflation_data'[Inflationrate])),
        FILTER(
            ALL('global_inflation_data'),
            VALUE('global_inflation_data'[Year]) = CurrentYear - 1
        )
    )
RETURN
IF(
    ISBLANK(PreviousInflationRate),
    BLANK(),
    DIVIDE(CurrentInflationRate - PreviousInflationRate, PreviousInflationRate)
)
