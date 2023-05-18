# Exploring Recipe Complexity Over Time

by Rio Aguina-Kang (raguinakang@ucsd.edu) and Judel Ancayan (jancayan@ucsd.edu)

---

## Introduction

In this project, we explored the relationship between time and the complexity of recipes. Using a dataset from <a href='https://www.food.com/'>food.com</a>, we gain access to 231,536 observations across 17 distinct features. To effectively evaluate recipe complexity, we utilized a key feature called "n_steps," which represents the number of steps required to prepare a recipe. Additionally, to investigate temporal trends, we considered the "submitted" date column, which encompasses recipe submissions spanning from 2008 to 2018. Finally, we utilized the "id" column to identify specific recipes within the dataset.

---

## Cleaning and Exploratory Data Analysis
**Data Cleaning**
To begin, we were provided with two different csv files, a csv containing recipe data and a csv containing interaction(comments and ratings) data. We imported both of these csvs as dataframes, and left merged the recipe dataframe and the interactions one on the recipe id columns. With the new dataframe, we changed the rating column so that all of the "0" values were now nan values, because these interactions represent comments, and have no rating. Following this, we added a column to the dataframe called 'average rating', which represented the average rating out of 5 that the recipe recived. Additionally, we typecasted the 'submitted' column(which is the date the recipe was submitted) and the 'date' column(which is when the comment was submitted) into the pandas datetime data type. To finish up cleaning the dataframe, we grouped the dataframe by id, and used the 'max' aggregate to preserve data per recipe, as well as ensure there were no duplicate recipes in the dataframe. The first few rows of the cleaned dataframe with all the listed changes is shown here(please note that the dataframe shown here is different from the dataframe used in the assessment of missingness. The dataframe used in that section is this dataframe before it was grouped by id, in order to preserve all of the separate interactions by recipe):

```py
print(unique_recipe.head()[['submitted','n_steps']].to_markdown(index=True))
```

|     id | submitted           |   n_steps |
|:-------|---------------------|----------:|
| 275022 | 2008-01-01 00:00:00 |        11 |
| 275024 | 2008-01-01 00:00:00 |         6 |
| 275026 | 2008-01-01 00:00:00 |         7 |
| 275030 | 2008-01-01 00:00:00 |        11 |
| 275032 | 2008-01-01 00:00:00 |         8 |

The above dataframe is a grouped dataframe, grouped by the year the recipe was submitted, with the aggregate function 'mean', displaying the mean of the columns that are able to have means.

**Univariate Analysis**

<iframe src="univariate_EDA.html" width=800 height=600 frameBorder=0></iframe>

The above graph charts the distribution of the number of steps each recipe has. The graph is right skewed, with majority of recipes having less than 20 steps, while there are a few recipes with upwards of 100 steps.


**Bivariate Analysis**

<iframe src="bivariate_EDA.html" width=800 height=600 frameBorder=0></iframe>

This line chart highlights the observed relation between the number of steps in a recipe and the year it was submitted. The graph shows a positive relation between the two (ignoring the drop in the year 2016, which could be considered an outlier), which suggests a positive correlation between the two, meaning that as the year increases, so does the average number of steps per recipe.

---

## Assessment of Missingness



---

## Hypothesis Testing

To answer the question of whether or not recipes have shown an increase in complexity over the last 10 years, we define our null and alternative hypotheses as such.

- **Null Hypothesis**: The average number of steps in 2018 is *the same* as in 2008, and any difference is a result of random chance

- **Alternative Hypothesis**: The average number of steps in 2018 is *greater* than it was in 2008. The observed difference in our samples cannot be explained by random chance alone.

To estimate an increase in recipe complexity between 2008 and 2018, we use a test statistic of the difference in mean number of steps between 2018 and 2008.

- **Test Statistic**: Difference in group means
<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mtext>mean number of steps in 2018</mtext>
  <mo>&#x2212;<!-- − --></mo>
  <mtext>mean number of steps in 2008</mtext>
</math> 

Since the distribution of recipe steps in 2008 is different from that of 2018, we run a permutation test. In this test, we generate new data by shuffling the "n_steps" column within the data to compute a single test statistic, calculating the differences in random distributions between recipe steps in 2018 and 2008. We do this over the course of 1000 trials, creating a new test statistic and appending it to an array of previous test statistics at each iteration. We also compute an observed test statistic from the original data

Here, we plotted the distribution of test statistics, as well as the obvserved test statistic noted as a red line in the plot below:

<iframe src="hypothesis_test.html" width=800 height=600 frameBorder=0></iframe>

Using the array of test statistics, we calculated the p-value by averaging the number of test statistics greater than our observed value, resulting in a p-value of 0.

Since the p-value is 0 and lower than the significance level of 0.05, we reject the null hypothesis that the number of steps in 2008 and the number of steps in 2018 come from the same distribution.

---