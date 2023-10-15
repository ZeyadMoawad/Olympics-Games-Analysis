# Olympics-Games-Analysis
![Screenshot 2023-10-15 071303](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/assets/96973429/9fc7f5ac-6191-4c79-b665-3c31a6e51497)
# Table of Contents
- [Problem Statement](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#problem-statement)
- [Data Sourcing](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#data-sourcing)
- [Data Preparation](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#data-preparation)
- [Data Modeling](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#data-modeling)
- [Data Visualization](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#data-visualization)
- [Data Analysis & Insights](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#data-analysis--insights)
- [Shareable link](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/edit/main/README.md#shareable-link)
  
  ---------------------------------------------
 # Problem Statement
 The purpose of this Olympic Games analysis is to visualize data that will help readers understand how countries have performed historically in the summer Olympic Games(with the possibility to select your own country). There is also an interest in the details about the competitors.
__________________________________
# Data Sourcing
- The Dataset used for this analysis is available at [Olympic Games dataset](https://www.dropbox.com/s/3sxwx52o3x8ozj7/olympic_games.bak?dl=0)
- ------------------------------------------------------
# Data Preparation
Data cleaning and transformation was done in Microsoft SQL Server and the datasets was loaded into Microsoft Power BI Desktop for modeling.

The Olympics Game dataset is contained in a table named:

  - Olympic_Data which has 11 columns and 222,552 rows of observation
The necessary data was first put into a SQL database and afterwards transformed using the transformations that you can see below.

Olympic_Data

```
SELECT
         [ID]
        ,[Name] AS 'Competitor Name'
        ,CASE WHEN SEX = 'M' THEN 'Male' ELSE 'Female' END AS Sex
        ,[Age]
		,CASE	WHEN [Age] < 18 THEN 'Under 18'
				WHEN [Age] BETWEEN 18 AND 25 THEN '18-25'
				WHEN [Age] BETWEEN 25 AND 30 THEN '25-30'
				WHEN [Age] > 30 THEN 'Over 30'
		 END AS [Age Grouping]
        ,[Height]
        ,[Weight]
        ,[NOC] AS 'Nation Code'
        ,LEFT(Games, CHARINDEX(' ', Games) - 1) AS 'Year' 
        ,[Sport]
        ,CASE WHEN Medal = 'NA' THEN 'Not Registered' ELSE Medal END AS Medal 
  FROM [olympic_games].[dbo].[athletes_event_results]
  WHERE RIGHT(Games,CHARINDEX(' ', REVERSE(Games))-1) = 'Summer'
  
```
# Data Modeling
After the dataset was cleaned and transformed, it was ready to be modeled(using Power BI Desktop).

- The fact and dimension have been combined into one table and is shown in the data model below
![Screenshot 2023-10-15 173810](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/assets/96973429/c42fc2d8-926a-4810-96bb-e6a7a9c0624e)
# Data Visualization
Data visualization for the dataset was done using Microsft Power BI Destop:
- The Olympic Games Analysis Page: Shows the # of competitors, # of Medals, # of medals by year, etc
Figure 1 shows visualizations from Olympic Games Analysis page
![Screenshot 2023-10-15 071303](https://github.com/ZeyadMoawad/Olympics-Games-Analysis/assets/96973429/cc4be3b3-bed3-4c52-8070-e14d8c6b5ff8)

---------------------
# Data Analysis & Insights
Measures used in visualization are:

- '# of Competitors' = DISTINTCOUNT ( 'Olympic_Data[ID] )

- '# of Medals' = COUNTROWS ( 'Olympic_Data' )

- '# of Medals (Registered)' = CALCULATE ([# of Medals], FILTER( 'Olympic_Data', 'Olympic_Data'[Medal] = "Bronze" || 'Olympic_Data' [Medal] = "Gold" || 'Olympic_Data'[Medal] = "Silver")

As shown from Data Visualization, It can be deduced that:

- From 1896-2016, the total number of competitors is 116,776
- From 1896-2016, the total number of medals received is 34,088
- -----------------------------------
# Shareable Link
You can interact with the report here:

[View Report](https://www.linkedin.com/feed/)

