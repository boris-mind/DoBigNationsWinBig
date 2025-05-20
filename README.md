# DoBigNationsWinBig

Welcome to my data portfolio **Do Big Nations Win Big**! This repository showcases my data analysis, visualizations, and projects that demonstrate my skills in working with data and deriving insights from various datasets.

## Table of Contents
- [About This Portfolio](#about-this-portfolio)
- [Technologies Used](#technologies-used)
- [Project Overview](#project-overview)
- [Project Details](#project-details)
- [How to View](#how-to-view)
- [Contact Information](#contact-information)

## About This Portfolio

This portfolio is a collection of my work on data analysis and visualizations. It highlights the methodologies I use, the tools I am proficient in, and the insights I've gathered from different datasets. The projects you’ll find here are all hosted on **Google Cloud Platform** and on **GitHub Pages** for easy viewing and sharing.

## Technologies Used

- **Power BI**
- **SQL**
- **Google Cloud Platform** for hosting
- **GitHub Pages** for hosting
- **HTML/CSS** for styling the webpage

## Project Overview

This project contains several analysis based on real-world data, including:
1. **Olympic Performance Analysis** - A deep dive into the Olympic Games history.
2. **Relationship between economic and OG Performance** - how economic factors such as GDP influence the performance of countries in the Olympic Games.
3. **FIFA World Cup Analysis** - A study of the relationship between GDP and success in the FIFA World Cup.
4. **Correlation between Population and OG Performance** - Insights into countries' population and athletic achievements.

If you prefer to watch a 2 minutes video instead of below, please click to this link to watch my presentation video.

## Project Details

### Data Sources

The datasets used in this project are sourced from Kaggle:
- https://www.kaggle.com/datasets/piterfm/olympic-games-medals-19862018
- https://www.kaggle.com/datasets/piterfm/fifa-football-world-cup
- https://www.kaggle.com/datasets/samithsachidanandan/gdp-by-country-1960-2023
- https://www.kaggle.com/datasets/iamsouravbanerjee/world-population-dataset

**Google Cloud Platform Storage**

Once the datasets were downloaded, they were uploaded to **Google Cloud Platform (GCP)**. I created a **bucket** in **Google Cloud Storage** to securely store the raw data, making it easily accessible for further processing.

Using **BigQuery**, I performed **SQL queries** on the data stored in the Cloud Storage bucket. This enabled me to process large datasets, transform them into structured tables, and optimize them for analysis. The processed tables were then made available for use in **Power BI**, where they were used for visualization and reporting.


**Introduction : Do Big Nations Win Big ?**

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB1.png)

**Who dominates the Games ?**

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB2.png)
![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB2.2.png)

Features and Techniques Used:

- Power BI > Power Query: Power BI > Power Query: Extracted the last 4 characters to obtain the Olympic year. For example, "tokyo-2020" becomes "2020".
- Power BI > Power BI Desktop: Created two bookmarks, "World View" and "Ranking View", and assigned buttons to each bookmark for interactive filter buttons.
- Power BI > DAX: Created a new table to aggregate the number of medals by country using DAX:

  *          DAX
          Copier
          MedaillesParPays = 
          SUMMARIZE(
              medals_df, 
              medals_df[country_name], 
              "TotalMedals", COUNT(medals_df[medal_type])
          )*

**GDP vs. Olympic Performance in 2016**

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB3.png)

Features and Techniques Used:

- Google Cloud Platform > Big Query: Create a GDP table for the year 2016 only

```SQL
CREATE TABLE `DoBigNationsWinBig.gdp_2016_only` AS
SELECT *
FROM `DoBigNationsWinBig.gdp_1960-2016`
WHERE Year = 2016;
```

**FIFA World Cup Performance by Year**

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB4.png)

Features and Techniques Used:

- Google Cloud Platform > Big Query: Correction des noms de pays "West Germany" by "Germany"

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
         
Dénormalisation des rôles : Les données sur le champion et le finaliste étaient dans une seule ligne (avec les colonnes "Champion" et "Runner-Up" côte à côte), le code ci-dessous a permis de créer deux lignes pour chaque année — une ligne pour le champion et une autre pour le finaliste. 

```SELECT Year, Champion AS Country, 'Champion' AS Role
FROM cleaned_world_cup

UNION ALL

SELECT Year, Runner_Up AS Country, 'Runner-Up' AS Role
FROM cleaned_world_cup
ORDER BY Year, Role;
```

**Population vs. Olympic Performance in 2016**

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB5.png)

Features and Techniques Used:

- Google Cloud Platform > Big Query: Create a table 

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

**Conclusion**

![Image loading error](https://github.com/boris-mind/DoBigNationsWinBig/blob/main/imageDBNWB6.png)

## How to View

This portfolio is hosted on **Google Cloud Platform**, **Power BI** and on **GitHub Pages**, and is accessible via the following URL:

[Visit my Data Portfolio 'Do Big Nations Win Big'](https://github.com/boris-mind/DoBigNationsWinBig)

Feel free to browse through the different projects and visualizations.

## Contact Information

If you have any questions or would like to discuss any of the projects, please reach out to me via:

- **Email**: your.email@example.com
- **LinkedIn**: [Your LinkedIn Profile](https://www.linkedin.com/in/)
- **GitHub**: [Your GitHub Profile](https://github.com/boris-mind)

Thank you for visiting my portfolio!
