# Pixar-films-Analysis
This SQL project examines a dataset of Pixar films obtained from Maven Analytics to understand their performance, audience reception, and evolution. By running structured SQL queries, the project uncovers insights that highlight both the business impact and the entertainment value of Pixar’s movies.

## Table of contents

- [Project Overview](https://github.com/DamilolaArogundade/Pixar-films-Analysis?tab=readme-ov-file#project-overview)
- [Project Scope](https://github.com/DamilolaArogundade/Pixar-films-Analysis#project-scope)
- [Business Objectives](https://github.com/DamilolaArogundade/Pixar-films-Analysis#business-objectives)
- [Document Purpose](https://github.com/DamilolaArogundade/Pixar-films-Analysis#business-objectives)
- [Use Case](https://github.com/DamilolaArogundade/Pixar-films-Analysis#use-case)
- [Dataset Overview](https://github.com/DamilolaArogundade/Pixar-films-Analysis#dataset-overview)
- Data Cleaning and Processing
- Data Analysis and Insight
- Recommendation
- Conclusion

## Project Overview
## Project Scope

The analysis focused on four main areas:

- Box Office Performance – Domestic, international, and worldwide sales compared to budgets.
- Awards Analysis – Number and type of awards won per film.
- Ratings Comparison – Multiple rating sources (Rotten Tomatoes, Metacritic, IMDB, CinemaScore).
- Trend Analysis – How genres and ratings have evolved over decades.
- Sequel vs. Original Analysis – Comparing franchise films like Cars, Toy Story, and The Incredibles.

## Business Objectives
  
The objective was to generate insights that could inform future film production and marketing strategies. Specifically, the analysis can help with:

- **Financial Insight**: Identify correlations between budget sizes and box office revenue.
- **Critical & Audience Insight**: Understand how awards and ratings interact (i.e., whether critical acclaim aligns with audience reception).
- **Franchise Analysis**: Evaluate the sustainability of sequels vs. originals for Pixar’s storytelling and profitability.
- **Historical Trends**: Map changes in film genres and average ratings across different decades to reveal shifts in Pixar’s creative direction.

## Document Purpose

This documentation translates technical SQL queries into a narrative of insights. The purpose is to:

- Provide non-technical stakeholders (executives, marketers, creatives) with a digestible summary of findings.
- Demonstrate the business and entertainment relevance of data-driven insights.
- Serve as a knowledge base for future Pixar-related analyses and comparisons with other studios.

## Use Case

The insights from this project can support:
- **Business Strategy**: Inform budget allocation for future Pixar films.
- **Creative Strategy**: Identify which genres and narratives resonate most over time.
- **Franchise Management**: Help decide whether sequels are worth pursuing based on past performance.
- **Marketing Teams**: Pinpoint what appeals most to audiences versus critics.
- **Entertainment Research**: Provide benchmarks for comparing Pixar with competitors like DreamWorks or Disney Animation.

## Dataset Overview

The dataset in use contains detailed information about Pixar films, sourced from Maven Analytics. It encompasses a comprehensive range of data points related to the box office performance, awards, genres, critical reception, and audience ratings of Pixar’s animated movies. The dataset covers films released over multiple decades, capturing both standalone titles and sequels.
This dataset serves as an invaluable resource for individuals seeking to practice data analysis techniques and to gain insights into the business and entertainment dimensions of film performance.

### Content and structure

 It consists of several interconnected tables, including
- **Box Office**: Revenue from U.S./Canada, international markets, worldwide totals, and film budgets.
- **Academy**: Awards and nominations received by each film.
- **Genres**: Classification of each film into categories such as Adventure, Animation, Comedy, and Family.
- **Pixar Films**: Core details such as film titles and release dates.
- **Pixar People**: Key contributors involved in each film.
- **Public Response**: Ratings from Rotten Tomatoes, Metacritic, IMDB, and CinemaScore.

With a relational structure across these tables, the dataset enables analysts to:

- Track financial performance trends across different markets.
- Examine the relationship between critical acclaim and audience response.
- Compare sequels with their original films in terms of ratings and success.
- Identify genre and rating evolution over time.

Overall, this dataset provides a robust foundation for practicing SQL queries and uncovering storytelling, marketing, and critical trends that have shaped Pixar’s legacy.

## Data Cleaning and Processing

After conducting data profiling, the dataset used for this analysis was found to be well-structured and consistent, with no significant issues that could impede analysis or interpretation. The data is in a standardized format, follows consistent naming conventions, and contains all required fields. The data values are accurate, columns are assigned appropriate data types, and there are no duplicate records.

The following procedures were carried out during the data processing phase.

- **Created Database:** A database named Pixar_films was created in SQL to house the tables imported from the dataset. That was done using the query below

``` SQL
  CREATE DATABASE Pixar_films
```

The queries below are used to display the tables and all the information contained within them.

``` SQL
Select *
From academy

Select *
From box_office

Select *
From genres

Select *
From pixar_films

Select *
From pixar_people

Select *
From public_response
```

- **Created relationships between tables:** Active relationships were created between tables using common columns (keys), where the table that has a column with the unique values has the primary key, and the table with the column related but does not have unique values has the foreign key. In SQL,  an active relationship serves as the default link between tables, which is used for filtering and calculations. 

A relationship was created between the box_office table and the academy table

Box_office table has a column with unique values, so box_office will have the primary key

```SQL
Alter table box_office
Add constraint pk_film_box_office
Primary key (film)  
```

To join the academy table, it will have a foreign key
``` SQL
Alter table academy
Add constraint fk_film_academy
Foreign key (film) references box_office (film)
```

A relationship was also created between the box_office table and the genres table

The genres table will also have a foreign key 
```SQL
Alter table genres
Add constraint fk_film_genres
Foreign key (film) references box_office (film)  
```

## Data Analysis and Insight

The objective of this analysis is to provide answers to the following questions:

-  Which films have performed the best at the box office? Did they have the highest budget?
- Which films received the most awards? Are they also the best rated?
- How do sequels compare to their original?
- Have genres and ratings evolved over time?

**1. Which films have performed the best at the box office? Did they have the highest budget?**

The main goal of these questions is to evaluate how Pixar movies performed at the box office and to analyze whether budget size influenced that performance. The results of this analysis will provide insights into whether investing in higher-budget productions leads to greater financial success, while also giving the company a clearer picture of how well its films have performed overall.

a. Which films have performed the best at the box office? 

To determine the movies' performances at the box offices, their performances at each box office will be evaluated. 

```SQL
Select top 1 film, box_office_us_canada
From box_office
Group by film, box_office_us_canada
Order by box_office_us_canada desc  
```

| Film | box_office_us_canada |
|------|----------------------|
| Inside Out 2 | 652980194 |


The result above shows that Inside Out 2 performed the best at the US/Canada box office.

```SQL
Select top 1 film, box_office_other
From box_office
Group by film, box_office_other
Order by box_office_other  desc
```
| Film | box_office_other |
|------|----------------------|
| Inside Out 2 | 1045050771 |

The result above shows that Inside Out 2 performed the best at other box offices.

 ```SQL
Select top 1 film, box_office_worldwide
From box_office
Group by film, box_office_worldwide
Order by box_office_worldwide desc
```
| Film | box_office_worldwide |
|------|----------------------|
| Inside Out 2 | 1698030965 |

The result above shows that Inside Out 2 performed the best at the worldwide box office

b. Did they have the highest budget?

To evaluate whether the top-performing movies at the box office were also the ones with the highest budgets, we first generate a list of films ranked by budget size. We then compare these results with the earlier findings on box office performance. This allows us to see if higher spending directly correlates with greater financial success. The SQL query below retrieves the movies with the largest budgets for this comparison.

```SQL
Select film, Budget
From box_office
Group by film,budget
Order by budget  desc
```
| Film | Budget |
|------|--------|
| Incredibles 2 | 200000000 |
| Finding Dory | 200000000 |
| Elemental | 200000000 |
| Cars 2 | 200000000 |
|Inside Out 2 | 200000000 |
| Lightyear | 200000000 |
| Monsters University | 200000000 |
| Toy Story 3 | 200000000 |
| Toy Story 4 | 200000000 |
| Brave | 185000000 |


The result above shows all the movies with the highest budgets, which are. Inside Out is one of the movies with the highest budgets.

In conclusion, Inside Out 2 achieved the strongest performance across all global box offices and also ranked among the films with the highest production budgets. This suggests that the significant investment contributed to its worldwide success

**2. Which films received the most awards? Are they also the best rated?**

The purpose of this analysis is to evaluate the performance of Pixar movies by examining both the number of awards they have won and their ratings across different review platforms. By comparing these two factors, we aim to understand whether strong ratings are a reliable indicator of award success or if award recognition can also influence how a film is rated.

a. Which films received the most awards

To determine the films that received the most awards, we will only filter out films that won an award(s) using the query below

```SQL
Select  film, award_type, [status]
From academy
Where [status] like 'w%'
Group by  film, award_type, [status]
```
| Film | Award type | Status |
|------|------------|--------|
| Brave | Animated Feature | Won |
| Coco | Animated Feature | Won |
| Coco | Original Song | Won |
| Finding Nemo | Animated Feature | Won |
| Inside Out | Animated Feature | Won |
| Monsters, Inc. | Original Song | Won |
| Ratatouille | Animated Feature | Won |
| Soul | Animated Feature | Won |
| Soul | Original Score | Won |
| The Incredibles | Animated Feature | Won |
| The Incredibles | Sound Editing | Won |
| Toy Story | Other | Won |
| Toy Story 3 | Animated Feature | Won |
| Toy Story 3 | Original Song | Won |
| Toy Story 4 | Animated Feature | Won |
| Up | Animated Feature | Won |
| Up | Original Score | Won |
| WALL-E | Animated Feature | Won |

```SQL
Select film, 
 Count ([status]) as number_of_awards_won
From  (Select film, award_type, [status]
      From academy
      Where [status] like 'w%'
      Group by film, award_type, [status]) as dd
Group by  film
Order by count ([status]) desc   
```
| Film | Number of awards won |
|------|----------------------|
| Coco | 2 |
| Soul | 2 |
| The Incredibles | 2 |
| Toy Story 3 | 2 |
| Up | 2 |
| WALL-E | 1 |
| Brave | 1 |
| Toy Story 4 | 1 |
| Toy Story | 1 |
| Finding Nemo | 1 |
| Inside Out | 1 |
| Monsters, Inc. | 1 |
| Ratatouille | 1 |

The results above show that Coco, Soul, The Incredibles, Toy Story 3, and Up received the most awards. Each won 2 awards.

The awards won table was saved in the database as an independent table using the query below

```SQL
Select *
Into awards_worn
From (Select film, 
    count ([status]) as number_of_awards_won
     From (Select film, award_type, [status]
      From academy
      Where [status] like 'w%'
      Group by film, award_type, [status]) as dd
       group by film) as dd
```

 b. Are they also the best rated?

```SQL
Select top 5 film, rotten_tomatoes_score
From public_response
Group by film, rotten_tomatoes_score
order by rotten_tomatoes_score desc   
```
| Film | rotten_tomatoes_score |
|------|-----------------------|
| Toy Story | 100 |
| Toy Story 2 | 100 |
| Finding Nemo | 99 |
| Inside Out | 98 |
| Toy Story 3 | 98 |


