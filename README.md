# DoBigNationsWinBig

Welcome to my data portfolio **Do Big Nations Win Big**! This repository showcases my data analysis, visualizations, and projects that demonstrate my skills in working with data and deriving insights from various datasets.

## Table of Contents
- [About This Project](#about-this-project)
- [Technologies Used](#technologies-used)
- [Project Overview](#project-overview)
- [Project Details](#project-details)
- [How to View](#how-to-view)
- [Contact Information](#contact-information)

## About This Project

This project is an overview of my work on data analysis and visualizations. It highlights the methodologies I use, the tools I am proficient in, and the insights I've gathered from different datasets. The projects you’ll find here are all hosted on **Google Cloud Platform** and on **GitHub Pages** for easy viewing and sharing.

## Technologies Used

- **Power BI / DAX**
- **SQL**
- **Google Cloud Platform** for hosting
- **GitHub Pages** for hosting

## Project Overview

This project contains several analysis based on real-world data, including:
1. **Olympic Performance Analysis** - A deep dive into the Olympic Games history.
2. **Relationship between economic and OG Performance** - How economic factors such as GDP influence the performance of countries in the Olympic Games.
3. **FIFA World Cup Analysis** - An exploration of the relationship between GDP and success in the FIFA World Cup.
4. **Correlation between Population and OG Performance** - Insights into countries' population and athletic achievements.

[![Please find a 6-minute video where I briefly demonstrate my data project in Power BI.](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWBvideo.png)](https://www.loom.com/share/fccf8fdfb234412483ebb64b7320896e?sid=4448521a-3c16-4312-bdc6-d23d31215c7a)

## Project Details

### Data Sources

The datasets used in this project are sourced from **Kaggle**:
- https://www.kaggle.com/datasets/piterfm/olympic-games-medals-19862018
- https://www.kaggle.com/datasets/piterfm/fifa-football-world-cup
- https://www.kaggle.com/datasets/samithsachidanandan/gdp-by-country-1960-2023
- https://www.kaggle.com/datasets/iamsouravbanerjee/world-population-dataset

### Google Cloud Platform Storage

Once the datasets were downloaded, they were uploaded to **Google Cloud Platform (GCP)**. I created a **bucket** in **Google Cloud Storage** to securely store the raw data, making it easily accessible for further processing.

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB0.png)

Using **BigQuery**, I performed **SQL queries** on the data stored in the Cloud Storage bucket. This enabled me to process large datasets, transform them into structured tables, and optimize them for analysis. The processed tables were then made available for use in **Power BI**, where they were used for visualization and reporting.

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB0.2.png)

### Introduction : Do Big Nations Win Big ?

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB1.png)

### The Olympic Games : Who dominates the Games ?

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB2.png)
![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB2.2.png)

Features and Techniques Used:

- **Power BI > Power Query: Power BI > Power Query:** Extracted the last 4 characters to obtain the Olympic year. For example, "tokyo-2020" becomes "2020".
- **Power BI > Power BI Desktop:** Created two bookmarks, "World View" and "Ranking View", and assigned buttons to each bookmark for interactive filter buttons.
- **Power BI > DAX:** Created a new table to aggregate the number of medals by country using DAX:

  *          DAX
          Copier
          MedaillesParPays = 
          SUMMARIZE(
              medals_df, 
              medals_df[country_name], 
              "TotalMedals", COUNT(medals_df[medal_type])
          )*

### GDP vs. Olympic Performance in 2016

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB3.png)

Features and Techniques Used:

- **Google Cloud Platform > Big Query:** Create a GDP table for the year 2016 only

```SQL
CREATE TABLE `DoBigNationsWinBig.gdp_2016_only` AS
SELECT *
FROM `DoBigNationsWinBig.gdp_1960-2016`
WHERE Year = 2016;
```

- **Power BI > Query :** Use first row as headers, delete columns, replace points with commas, replace Country Name, change the year format to fixed decimal number etc.
- **Power BI > Desktop :** Create a measure that counts the total number of medals for the year 2016 using DAX.

 *          DAX
          Copier
          TotalMedals_2016 = 
          CALCULATE(
              COUNT('olympic_medals_1896-2022'[medal_type]),
        'olympics_medals_1896-2022'[slug_game] = "rio-2016"
          )*

### FIFA World Cup Performance by Year

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB4.png)

Features and Techniques Used:

- **Google Cloud Platform > Big Query:** Correction of country names: 'West Germany' replaced by 'Germany'

```SQL
  WITH cleaned_world_cup AS (
  SELECT 
    Year,
    CASE 
      WHEN Champion = 'West Germany' THEN 'Germany'
      ELSE Champion
    END AS Champion,
    
    CASE 
      WHEN `Runner-Up` = 'West Germany' THEN 'Germany'
      ELSE `Runner-Up`
    END AS Runner_Up
  FROM `endless-gasket-*********.DoBigNationsWinBig.world_cup`
)
```
         
**Denormalization of Roles:** The data for the champion and the runner-up were in a single row (with the "Champion" and "Runner-Up" columns side by side). The code below was used to create two rows for each year — one for the champion and another for the runner-up.

```SELECT Year, Champion AS Country, 'Champion' AS Role
FROM cleaned_world_cup

UNION ALL

SELECT Year, Runner_Up AS Country, 'Runner-Up' AS Role
FROM cleaned_world_cup
ORDER BY Year, Role;
```

### Population vs. Olympic Performance in 2016

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB5.png)

Features and Techniques Used:

- **Google Cloud Platform > Big Query:** Create a table keeping only the year 2015

```SQL
CREATE TABLE `DoBigNationsWinBig.world_population_2015` AS
SELECT 
    Country,
    `2015 Population`,
    `Area km`
FROM 
    `DoBigNationsWinBig.world_population`
ORDER BY 
    `2015 Population` DESC;
```

### Conclusion

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB6.png)

## How to View

This portfolio is hosted on **Google Cloud Platform**, **Power BI** and on **GitHub Pages**, and is accessible via the following URL:

[Visit my Data Portfolio 'Do Big Nations Win Big'](https://github.com/boris-mind/DoBigNationsWinBig)

## Contact Information

If you have any questions or would like to discuss any of the projects, please reach out to me via:

- **Email**: boris.kang.ly@gmail.com
- **LinkedIn**: [Your LinkedIn Profile](https://www.linkedin.com/in/)
- **GitHub**: [Your GitHub Profile](https://github.com/boris-mind)

Thank you for visiting my portfolio!
