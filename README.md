# Exploring Recipe Complexity Over Time

by Rio Aguina-Kang (raguinakang@ucsd.edu) and Judel Ancayan (jancayan@ucsd.edu)

---

## Introduction

In this project, we explored the relationship between time and the complexity of recipes. Using a dataset from <a src='https://www.food.com/'>food.com</a>, we gain access to 231,536 observations across 17 distinct features. To effectively evaluate recipe complexity, we utilized a key feature called "n_steps," which represents the number of steps required to prepare a recipe. Additionally, to investigate temporal trends, we considered the "submitted" date column, which encompasses recipe submissions spanning from 2008 to 2018. Finally, we utilized the "id" column to identify specific recipes within the dataset.

---

## Cleaning and EDA
<h2>Data Cleaning</h2>
To begin, we were provided with two different csv files, a csv containing recipe data and a csv containing interaction(comments and ratings) data. We imported both of these csvs as dataframes, and left merged the recipe dataframe and the interactions one on the recipe id columns. With the new dataframe, we changed the rating column so that all of the "0" values were now nan values, because these interactions represent comments, and have no rating. Following this, we added a column to the dataframe called 'average rating', which represented the average rating out of 5 that the recipe recived. Additionally, we typecasted the 'submitted' column(which is the date the recipe was submitted) and the 'date' column(which is when the comment was submitted) into the pandas datetime data type. To finish up cleaning the dataframe, we grouped the dataframe by id, and used the 'max' aggregate to preserve data per recipe, as well as ensure there were no duplicate recipes in the dataframe. The first few rows of the cleaned dataframe with all the listed changes is shown here(please note that the dataframe shown here is different from the dataframe used in the assessment of missingness. The dataframe used in that section is this dataframe before it was grouped by id, in order to preserve all of the separate interactions by recipe):
|     id | submitted           |   n_steps |
|-------:|:--------------------|----------:|
| 275022 | 2008-01-01 00:00:00 |        11 |
| 275024 | 2008-01-01 00:00:00 |         6 |
| 275026 | 2008-01-01 00:00:00 |         7 |
| 275030 | 2008-01-01 00:00:00 |        11 |
| 275032 | 2008-01-01 00:00:00 |         8 |
The above dataframe is a grouped dataframe, grouped by the year the recipe was submitted, with the aggregate function 'mean', displaying the mean of the columns that are able to have means.
<iframe src="assets/10-80-enrollment.html" width=800 height=600 frameBorder=0></iframe>

---

## Assessment of Missingness

Here's what a Markdown table looks like. Note that the code for this table was generated _automatically_ from a DataFrame, using

```py
print(counts[['Quarter', 'Count']].head().to_markdown(index=False))
```

| Quarter     |   Count |
|:------------|--------:|
| Fall 2020   |       3 |
| Winter 2021 |       2 |
| Spring 2021 |       6 |
| Summer 2021 |       4 |
| Fall 2021   |      55 |

---

## Hypothesis Testing


---