# Pixar-films-Analysis
This SQL project examines a dataset of Pixar films obtained from Maven Analytics to understand their performance, audience reception, and evolution. By running structured SQL queries, the project uncovers insights that highlight both the business impact and the entertainment value of Pixar’s movies.

## Table of contents

- [Project Scope](https://github.com/DamilolaArogundade/Pixar-films-Analysis#project-scope)
- [Business Objectives](https://github.com/DamilolaArogundade/Pixar-films-Analysis#business-objectives)
- [Document Purpose](https://github.com/DamilolaArogundade/Pixar-films-Analysis#business-objectives)
- [Use Case](https://github.com/DamilolaArogundade/Pixar-films-Analysis#use-case)
- [Dataset Overview](https://github.com/DamilolaArogundade/Pixar-films-Analysis#dataset-overview)
- [Data Cleaning and Processing](https://github.com/DamilolaArogundade/Pixar-films-Analysis?tab=readme-ov-file#data-cleaning-and-processing)
- [Data Analysis and Insight](https://github.com/DamilolaArogundade/Pixar-films-Analysis?tab=readme-ov-file#data-analysis-and-insight)
- Recommendation
- Conclusion

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

### 1. Which films have performed the best at the box office? Did they have the highest budget?

The main goal of these questions is to evaluate how Pixar movies performed at the box office and to analyze whether budget size influenced that performance. The results of this analysis will provide insights into whether investing in higher-budget productions leads to greater financial success, while also giving the company a clearer picture of how well its films have performed overall.

**a. Which films have performed the best at the box office?**

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

**b. Did they have the highest budget?**

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

### 2. Which films received the most awards? Are they also the best rated?

The purpose of this analysis is to evaluate the performance of Pixar movies by examining both the number of awards they have won and their ratings across different review platforms. By comparing these two factors, we aim to understand whether strong ratings are a reliable indicator of award success or if award recognition can also influence how a film is rated.

**a. Which films received the most awards**

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

An SQL query was then written to calculate the total number of awards won by each movie, allowing for a clearer comparison of award performance across all films.

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

 **b. Are they also the best rated?**

To determine whether the movies that won the most awards are also the highest-rated, we analysed film ratings across all available review criteria. Then we compared these results with the list of top award-winning films.

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

The results above show that Toy Story and Toy Story 2 are the top-rated movies according to the Rotten Tomatoes criteria. Using this criterion, the movies that won awards are not the best rated.


```SQL
Select top 5 film, metacritic_score
From public_response
Group by film, metacritic_score
order by metacritic_score desc     
```
| Film | metacritic_score |
|------|------------------|
| Ratatouille | 96 |
| Toy Story | 95 |
| WALL-E | 95 |
| Inside Out | 94 |
| Toy Story 3 | 92 |

The result above shows that Ratatouille is the top-rated movie using the Metacritic criteria. Using this criterion, the movies that won awards are not the best rated.


```SQL
Select top 5 film, imdb_score
From  public_response
Group by film, imdb_score
order by imdb_score desc 
```

| Film | imdb_score |
|------|------------|
| Coco | 8.39999961853027 |
| WALL-E | 8.39999961853027 |
| Toy Story | 8.30000019073486 |
| Toy Story 3 | 8.30000019073486 |
| Up | 8.30000019073486 |

The result above shows that Coco and Wall-E are the top-rated movies using the IMDb criteria. Using this criterion, Coco won the most awards and was also the best rated.


```SQL
Select *
Into IMDB_criteria
From (Select film, imdb_score
     From public_response
      Group by film, imdb_score) as dd   
```

```SQL
Select film, cinema_score, Cinema_score_no
From public_response
Group by film, cinema_score, Cinema_score_no
order by Cinema_score_no asc       
```

| Film | Cinema score | Cinema score number |
|------|--------------|---------------------|
| Coco | A+| 1 |
| Finding Nemo | A+ | 1 |
| Incredibles 2 | A+ | 1 |
| Monsters, Inc. | A+ | 1 |
| The Incredibles | A+ | 1 |
| Toy Story 2 | A+ | 1 |
| Up | A+ | 1 |
| A Bug's Life | A | 2 |
| Brave | A | 2 |
| Cars | A | 2 |

These are the best-rated movies according to the CinemaScore criteria. Coco, Finding Nemo, Incredibles 2, Monsters Inc., The Incredibles, Toy Story 2, and Up are the top-rated movies.

```SQL
Select *
Into Cinema_criteria
From (Select film, cinema_score, Cinema_score_no
      From public_response
      Group by film, cinema_score, Cinema_score_no) as dd 
```

The query above is used to save the CinemaScore table in the database for further reference.

A relationship was created between cinema criteria and awards won for further analysis.

```SQL
Alter table Cinema_criteria
Add constraint Pk_film_cinema_criteria
Primary key (film)
```

```SQL
Alter Table awards_worn
Add constraint Fk_film_awards_worn
Foreign key (film) references cinema_criteria (film)
```

```SQL
Select top 3 awards_worn.film, number_of_awards_won, cinema_score
From awards_worn
inner join Cinema_criteria
on
awards_worn.film = Cinema_criteria.film
Where cinema_score = 'A+'
group by awards_worn.film, number_of_awards_won, cinema_score
Order by number_of_awards_won desc              
```

The Query above is used to compare the movies that won awards and the CinemaScore table to show if the movies that won awards are also the best rated.

| Film | Number of awards won | Cinema score |
|------|----------------------|--------------|
| Coco | 2 | A+ |
| The Incredibles | 2 | A+ |
| Up | 2 | A+ |

The result above shows that Coco, The Incredibles, and Up won the most awards and were also the best rated.

### 3. How do sequels compare to their originals?

The purpose of this analysis is to evaluate how well each sequel performed compared to its original film. By comparing their box office results, ratings, and awards, we can assess whether producing sequels is a worthwhile investment or identify potential factors that contributed to underperformance. The films included in this analysis are Cars, Finding Nemo and Finding Dory, Inside Out, Monsters, Inc. and Monsters University, The Incredibles, and Toy Story.

To analyze this, a relationship was created between the box office table and the academy to see their performances compared to the sequels

```SQL
Alter table public_response
Add constraint FK_film_public_response
Foreign key (film) references box_office (film) 
```

```SQL
Select Box_office.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide
From box_office
Inner join public_response
on
box_office.film = public_response.film
Group by box_office.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide
```

A new table titled “Ratings and Box Office Performance” was created and stored in the database using the query below. This table was derived from the relationship established between the Box Office and Awards tables, allowing for easier analysis of how financial success relates to award achievements.

```SQL
Select *
Into Ratings_and_box_office_performance
From (Select Box_office.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide
       From box_office
       Inner join public_response
         on
       box_office.film = public_response.film
       Group by box_office.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide) as dd
```

Another relationship was established between the ratings and box office performance table and the awards table to provide a more comprehensive view of each film’s overall success from multiple perspectives—financial, critical, and audience-based, using the query below.

```SQL
Alter table Ratings_and_box_office_performance
Add constraint pk_film_Ratings_and_box_office_performance
Primary key (film)
```

```SQL
Select Ratings_and_box_office_performance.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide, number_of_awards_won
From Ratings_and_box_office_performance
Inner join awards_worn
on
Ratings_and_box_office_performance.film = awards_worn.film
Group by Ratings_and_box_office_performance.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide, number_of_awards_won
```

The new derived is named 'Relationship table' and saved in the database as an independent table for further analysis using the query below

```SQL
Select *
Into relationship_table
From (Select Ratings_and_box_office_performance.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide, number_of_awards_won
From Ratings_and_box_office_performance
Inner join awards_worn
on
Ratings_and_box_office_performance.film = awards_worn.film
Group by Ratings_and_box_office_performance.film, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score, box_office_us_canada, box_office_other, box_office_worldwide, number_of_awards_won) as dd
```

**Cars**

Beginning with the first film that has a sequel—Cars—the analysis focuses on the Ratings and Box Office Performance table, as none of the films in this series received any awards. This allows us to evaluate their performance based solely on financial results and audience ratings.

```SQL
Select *
From Ratings_and_box_office_performance[dbo]
Where film like 'car%'    
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|
| Cars | 75 | 73 | A | 7.19999980926514 | 244082982 | 217900167 | 461983149 |
| Cars 2 | 40 | 57 | A- | 6.19999980926514 | 191452396 | 368400000 | 559852396 |
| Cars 3 | 69 | 59 | A | 6.69999980926514 | 152901115 | 231029541 | 383930656 |

From the analysis above, the original Cars movie outperformed its sequels across all evaluation criteria. It achieved higher ratings on every review platform and recorded the strongest performance in both domestic and international box offices.

**Finding Nemo and Finding Dory**

Finding Nemo is the original, while Finding Dory is the sequel. The analysis incorporates all available performance metrics using both the ratings and box office performance table and the relationship table to provide a comprehensive comparison between the two movies.

```SQL
Select *
From Ratings_and_box_office_performance
Where film like 'Finding%'     
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|
| Finding Dory | 94 | 77 | A | 7.19999980926514 | 486295561 | 542275328 | 1028570889 |
| Finding Nemo | 99 | 90 | A+ | 8.19999980926514 | 339714978 | 531300000 | 871014978 |

```SQL
Select *
From relationship_table
Where film like 'Finding%'     
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide | number_of_awards_won |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|----------------------|
| Finding Nemo | 99 | 90 | A+ | 8.19999980926514 | 339714978 | 531300000 | 871014978 | 1 |

From the analysis above, Finding Nemo (the original) outperformed Finding Dory in most criteria and also received an award, indicating stronger overall critical and audience reception.

**Inside Out**

For the Inside Out films, Inside Out is the original, and Inside Out 2 is the sequel. The analysis will be done using both the ratings and the box office performance table and the relationship table to provide a comprehensive comparison between the two movies.

```SQL
Select *
From Ratings_and_box_office_performance
Where film like 'inside%'  
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|
| Inside Out | 98 | 94 | A | 8.10000038146973 | 356461711 | 501149463 | 857611174 |
| Inside Out 2 | 90 | 73 | A | 7.59999990463257 | 652980194 | 1045050771 | 1698030965 |

```SQL
Select *
From relationship_table
Where film like 'inside%'     
```
| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide | number_of_awards_won |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|----------------------|
| Inside Out | 98 | 94 | A | 8.10000038146973 | 356461711 | 501149463 | 857611174 | 1 |

From the analysis above, while Inside Out 2 achieved higher box office revenue, the original Inside Out received better ratings across most platforms and also earned an award. This suggests that the original film had a greater critical impact, even if the sequel performed better commercially.

**Toy Story**

For the Toy Story collections, Toy Story being the original, the analysis will be done using both the ratings and box office performance table and the relationship table to provide a comprehensive comparison between all the movies.

```SQL
Select *
From Ratings_and_box_office_performance
Where film like 'toy%' 
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|
| Toy Story | 100 | 95 | A | 8.30000019073486 | 223225679 | 171210907 | 394436586 |
| Toy Story 2 | 100 | 88 | A+ | 7.90000009536743 | 245852179 | 265506097 | 511358276 | 
| Toy Story 3 | 98 | 92 | A | 8.30000019073486 | 415004880 | 651964823 | 1066969703 |
| Toy Story 4 | 97 | 84 | A | 7.59999990463257 | 434038008 | 639356585 | 1073394593 |

```SQL
Select *
From relationship_table
Where film like 'toy%'
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide | number_of_awards_won |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|----------------------|
| Toy Story | 100 | 95 | A | 8.30000019073486 | 223225679 | 171210907 | 394436586 | 1 |
| Toy Story 3 | 98 | 92 | A | 8.30000019073486 | 415004880 | 651964823 | 1066969703 | 2 |
| Toy Story 4 | 97 | 84 | A | 7.59999990463257 | 434038008 | 639356585 | 1073394593 | 1 |

From the analysis above, the original Toy Story maintained higher ratings on most review platforms, while Toy Story 3 received more awards. This reflects how later sequels can achieve strong recognition despite slightly lower ratings.

**Monsters, Inc. and Monsters University**

For the movies Monsters, Inc. and Monsters University, Monsters, Inc. being the original and Monsters University being the sequel, the analysis will be done using both the ratings and box office performance table and the relationship table to provide a comprehensive comparison between the two movies.

```SQL
Select *
From Ratings_and_box_office_performance
Where film like 'monster%' 
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|
| Monsters University | 80 | 65 | A | 7.19999980926514 | 268492764 | 475066843 | 743559607 |
| Monsters, Inc. | 96 | 79 | A+ | 8.10000038146973 | 255873250 | 272900000 | 528773250 |

```SQL
Select *
From relationship_table
Where film like 'monster%'
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide | number_of_awards_won |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|----------------------|
| Monsters, Inc. | 96 | 79 | A+ | 8.10000038146973 | 255873250 | 272900000 | 528773250 | 1 |

From the analysis above, the results reveal that Monsters, Inc. (the original) performed better in most rating categories and also won an award, suggesting that the first film had a stronger critical and emotional connection with audiences than its sequel.

**The Incredibles**

For the Incredibles collection —The Incredibles as the original and Incredibles 2 as the sequel — the analysis incorporated the Ratings, Awards, and Box Office Performance tables.

```SQL
Select *
From Ratings_and_box_office_performance
Where film like '%incredible%' 
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|
| Incredibles 2 | 93 | 80 | A+ | 7.5 | 608581744 | 634223615 | 1242805359 |
| The Incredibles | 97 | 90 | A+ | 8 | 261441092 | 370001000 | 631442092 |

```SQL
Select *
From relationship_table
Where film like '%incredible%'
```

| Film | rotten_tomatoes_score | metacritic_score | cinema_score | imdb_score | box_office_us_canada | box_office_other | box_office_worldwide | number_of_awards_won |
|------|-----------------------|------------------|--------------|------------|----------------------|------------------|----------------------|----------------------|
| The Incredibles | 97 | 90 | A+ | 8 | 261441092 | 370001000 | 631442092 | 2 |

The analysis above shows that the original Incredibles film outperformed the sequel in ratings and received two awards, while Incredibles 2 generated higher box-office revenue. This demonstrates how sequels may achieve greater commercial success but not always match the critical acclaim of their predecessors.


### 4. Have genres and ratings evolved over time?

The purpose of this analysis is to examine how the genres of Pixar films have evolved to identify whether certain genres have remained consistent or if there has been a mix of new and changing themes. It also aims to analyze how movie ratings have trended over the years, determining whether audience and critic scores have improved, declined, or remained steady across different time periods.

**Genres Evolution**

To achieve this, a relationship was established between the Genres table and the Pixar Films table to combine all relevant information into a single dataset, allowing for a more comprehensive analysis of genre trends over time using the query below

```SQL
Alter table pixar_films
Add constraint pk_film_pixar_films
Primary key (film)    
```

```SQL
Select pixar_films.film, release_date,category,[value]
From pixar_films
Inner join genres
on
pixar_films.film = genres.film
```

Then the table is saved into the database as Genre_overtime using the query below

```SQL
Select *
Into Genre_overtime
From (Select pixar_films.film, release_date,category,[value]
       From pixar_films
       Inner join genres
        on
        pixar_films.film = genres.film) as dd
```

```SQL
Select film, release_date,
       count (case when [value] = 'adventure' then 1 end) as adventure,
	   count (case when [value] = 'Animation' then 1 end) as animation,
	   count (case when [value] = 'comedy' then 1 end) as comedy,
	   count (case when [value] = 'Action' then 1 end) as [action],
	   count (case when [value] = 'drama' then 1 end) as drama,
	   count (case when [value] = 'Family' then 1 end) as family
From Genre_overtime
Group by film, release_date
Order by release_date asc  
```

| Film | release_date | adventure | animation | comedy | action | drama | family |
|------|--------------|-----------|-----------|--------|--------|-------|--------|
| Toy Story | 1995-11-22 | 1 | 1 | 1 | 0 | 0 | 0 | 
| A Bug's Life | 1998-11-25 | 1 | 1 | 1 | 0 | 0 | 0 |
| Toy Story 2 | 1999-11-24 | 1 | 1 | 1 | 0 | 0 | 0 |
| Monsters, Inc. | 2001-11-02 | 1 | 1 | 1 | 0 | 0 | 0 |
| Finding Nemo | 2003-05-30 | 1 | 1 | 1 | 0 | 0 | 0 |
| The Incredibles | 2004-11-05 | 1 | 1 | 0 | 1 | 0 | 0 |
| Cars | 2006-06-09 | 1 | 1 | 1 | 0 | 0 | 0 |
| Ratatouille | 2007-06-29 | 1 | 1 | 1 | 0 | 0 | 0 |
| WALL-E | 2008-06-27 | 1 | 1 | 0 | 0 | 0 | 1 |
| Up | 2009-05-29 | 1 | 1 | 1 | 0 | 0 | 0 |
| Toy Story 3 | 2010-06-18 | 1 | 1 | 1 | 0 | 0 | 0 |
| Cars 2 | 2011-06-24 | 1 | 1 | 1 | 0 | 0 | 0 |
| Brave | 2012-06-22 | 1 | 1 | 0 | 1 | 0 | 0 |
| Monsters University | 2013-06-21 | 1 | 1 | 1 | 0 | 0 | 0 |
| Inside Out | 2015-06-19 | 1 | 1 | 1 | 0 | 0 | 0 |
| The Good Dinosaur | 2015-11-25 | 1 | 1 | 0 | 1 | 0 | 0 |
| Finding Dory | 2016-06-17 | 1 | 1 | 1 | 0 | 0 | 0 |
| Cars 3 | 2017-06-16 | 1 | 1 | 1 | 0 | 0 | 0 |
| Coco | 2017-11-22 | 1 | 1 | 0 | 0 | 1 | 0 |
| Incredibles 2 | 2018-06-15 | 1 | 1 | 0 | 1 | 0 | 0 |
| Toy Story 4 | 2019-06-21 | 1 | 1 | 1 | 0 | 0 | 0 |
| Onward | 2020-03-06 | 1 | 1 | 1 | 0 | 0 | 0 |
| Soul | 2020-12-25 | 1 | 1 | 1 | 0 | 0 | 0 |
| Luca | 2021-06-18 | 1 | 1 | 1 | 0 | 0 | 0 |
| Turning Red | 2022-03-11 | 1 | 1 | 1 | 0 | 0 | 0 |
| Lightyear | 2022-06-17 | 1 | 1 | 0 | 1 | 0 | 0 |
| Elemental | 2023-06-16 | 1 | 1 | 1 | 0 | 0 | 0 |
| Inside Out 2 | 2024-06-14 | 1 | 1 | 1 | 0 | 0 | 0 |

From the analysis above, it was observed that the adventure and animation genres have remained consistent throughout the years, appearing in all Pixar films. The comedy genre, however, has shown less consistency, while other genres such as action, drama, and family appear only occasionally over time.

**Ratings evolution**

To achieve this, a relationship was established between the public response table and the Pixar Films table to combine all relevant information into a single dataset, allowing for a more comprehensive analysis of the ratings over time using the query below

```SQL
Select pixar_films.film, release_date, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score
From pixar_films
Inner join public_response
on
pixar_films.film = public_response.film
```

The table is saved as Ratings_oertime into the database using the query below

```SQL
Select *
Into ratings_overtime
From (Select pixar_films.film, release_date, rotten_tomatoes_score, metacritic_score, cinema_score, imdb_score
        From pixar_films
      Inner join public_response
       on
        pixar_films.film = public_response.film) as dd
```

A new column named release_year was added to the Ratings_overtime table to derive the year each movie was released from the dat column using the query below

```SQL
Alter table Ratings_overtime
add release_year varchar(50)
```

```SQL
Update ratings_overtime
set release_year = datename (year, release_date) 
```

The query below was used to analyse the average ratings in the 90s

```SQL
Select 
    avg(rotten_tomatoes_score) as avg_rotten,
	avg(metacritic_score) as avg_metacritic,
	avg(imdb_score) as avg_imdb
From ratings_overtime
Where release_year like '19%'  
```

| avg_rotten | avg_metacritic | avg_imdb |
|------------|----------------|----------|
| 97 | 87 | 7.80000003178914 |

The query below is used to determine the average ratings in the next decade, that is, 2001-2010

```SQL
Select 
    avg(rotten_tomatoes_score) as avg_rotten,
	avg(metacritic_score) as avg_metacritic,
	avg(imdb_score) as avg_imdb
From ratings_overtime
Where release_year in (2001,2002,2003,2004,2005,2006,2007,2008,2009,2010)
```

| avg_rotten | avg_metacritic | avg_imdb |
|------------|----------------|----------|
| 94 | 87 | 8.07500004768372 |

The query below is used to determine the average ratings in the next decade, that is, 2011-2020

```SQL
Select 
    avg(rotten_tomatoes_score) as avg_rotten,
	avg(metacritic_score) as avg_metacritic,
	avg(imdb_score) as avg_imdb
From ratings_overtime
Where release_year in (2011,2012,2013,2014,2015,2016,2017,2018,2019,2020)  
```
| avg_rotten | avg_metacritic | avg_imdb |
|------------|----------------|----------|
| 83 | 73 | 7.34166657924652 |

The query below is used to determine the average ratings in the next years, that is, 2021-2024

```SQL
Select 
    avg(rotten_tomatoes_score) as avg_rotten,
	avg(metacritic_score) as avg_metacritic,
	avg(imdb_score) as avg_imdb
From ratings_overtime
Where release_year in (2021,2022,2023,2024) 
```

| avg_rotten | avg_metacritic | avg_imdb |
|------------|----------------|----------|
| 84 | 69 | 7.01999998092651 |

From this analysis
- It was observed that Pixar films released in the 1990s recorded the highest average ratings on Rotten Tomatoes and Metacritic.
- In the following decade (2001–2010), the average ratings declined compared to the 1990s, although IMDb scores were at their highest during this period. 
- Between 2011 and 2020, the overall average ratings continued to decline across all platforms.
- However, in the most recent years (2021–2024), there was a slight improvement in Rotten Tomatoes ratings, while other rating platforms showed a further decrease.

Overall, the analysis shows that Pixar’s film ratings have gradually declined over the years. Movies released in the 1990s received the highest critical acclaim, reflecting strong audience and critic approval during that era. In the following decades, however, there has been a steady decrease in average ratings across most review platforms. While the 2021–2024 period shows a modest improvement on Rotten Tomatoes, the overall trend indicates that Pixar’s more recent films are receiving more varied and less consistent feedback compared to their earlier successes.

## Recommendations

- **Focus on Original Content:** The data shows that Pixar’s original movies generally perform better than sequels in ratings and awards. Focusing on fresh ideas and unique storytelling can help the studio maintain its creative edge.
- **Invest Wisely in High-Budget Productions:** High-budget films often bring in the best box office results, but not all expensive movies perform equally well. Pixar should continue investing in big projects while using data insights to guide where the money will have the most impact.
- **Sustain Strong Genres:** Adventure and Animation remain Pixar’s strongest and most consistent genres. The studio should continue building on these strengths while carefully exploring new ideas aligned with audience trends.
- **Enhance Audience and Critic Alignment:** Ratings have slightly dropped over time, suggesting that audience expectations have changed. Pixar can use audience feedback and review data to better understand what today’s viewers connect with emotionally.
- **Adopt Data-Driven Planning:** Pixar should make data part of its everyday planning—using it to predict how films might perform, monitor results, and make faster, more informed decisions for future projects.

## Conclusion

This project successfully demonstrated how SQL can be used to draw actionable insights from entertainment data. Key takeaways include the positive correlation between budget and box office success, the general superiority of original films over sequels, and genre/rating trends over time. These findings provide a foundation for making strategic decisions in content creation, budgeting, and marketing within the animation industry.

Thank you for viewing this project. I completed this project to showcase my data analysis skills using a data set from a fictitious company from Mavin Analystics. I am actively seeking data analyst roles and am open to new opportunities. If you are interested in discussing opportunities or have any feedback, I would love to hear from you.

### Contact me

**Email:** Raimotarogundade@gmail.com

**LinkedIn:** 
