# World Population Analysis

## Overview
This project aims to analyze world population data to uncover trends, patterns, and insights that can inform policy-making, economic planning, and various other applications. The analysis is performed using SQL, leveraging its powerful querying capabilities to manage and manipulate the dataset effectively.

## Data Source
The data used for this project comes from the United Nations World Population Prospects database. This dataset includes comprehensive demographic data from countries around the world, spanning several decades.

## Tools
- Microsoft Excel for Data Cleaning
- Microsoft SQL Server for Data Analysis

## Data Cleaning/Preparation
- Data Import: Importing the dataset into the RDBMS.
- Data Normalization: Ensuring consistency in data formats (e.g., date formats, numeric formats).
- Missing Values: Handling missing values through imputation or removal, as appropriate.
- Data Transformation: Creating new columns or modifying existing ones to facilitate analysis (e.g., calculating population growth rates).
- Indexing: Adding indexes to improve query performance.

## Exploratory Data Analysis

Exploratory Data Analysis (EDA) involves:

- Summary Statistics:
Calculating measures such as mean, median, and standard deviation to understand the distribution of data.
- Data Visualization:
Generating charts and graphs to identify trends and outliers. This includes plotting population growth over time and comparing population distributions across regions.
- Correlation Analysis:
Identifying relationships between different demographic variables (e.g., fertility rate vs. life expectancy).

## Data Analysis

- To find top 10 countries with high density of population

```SQL
SELECT
	TOP 10 Country,
	Density,
	[Land Area],
	Population
FROM Population
ORDER BY Density DESC;
```
- To group the countries based on their fertility rate

```SQL
SELECT Country, [Fertility Rate],
CASE
	WHEN [Fertility Rate]>=4.5 THEN 'High'
	WHEN [Fertility Rate]>=2.5 THEN 'Medium'
	ELSE 'Low'
END AS Category
FROM Population;
```
- To group countries based on the median average
```SQL
SELECT Country, [Median Age],
CASE
	WHEN [Median Age]>40 THEN 'Old'
	WHEN [Median Age]>20 THEN 'Young'
	ELSE 'Teenagers'
END AS [Country's Age]
FROM Population;
```
- To assign rank to countries based on their GDP per capita and GDP growth rate
```SQL
SELECT
	P.Country,
	P.Population,
	G.[GDP Per Capita],
	DENSE_RANK() OVER(ORDER BY G.[GDP Per Capita] DESC) AS [GDP Rank],
	DENSE_RANK()OVER(ORDER BY [GDP Growth] DESC) AS [Growth Rank]
FROM Population P
JOIN GDP G ON P.Country = G.Country
ORDER BY P.Population DESC;
```


## Results/Findings
The analysis results are summerized as follows:
- GDP growth is more in Asian countries as compared to western in the recent trends
- Density of population is also more in Asian countries as compared to most of the western countries
- India has shown tremendous potential to grow in the past few years


Author
                    
                    Created by Ketan W
