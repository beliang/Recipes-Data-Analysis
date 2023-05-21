# __Calorics Differences in Foods With High Sugar vs Carbs__

## Introduction

Our dataset for this data analysis project contains 2 CSVs from [food.com](https://www.food.com/). One of the CSV contains recipe information with a unique ID to each unique recipe and the other CSV contains user data about their ratings and reviews on a recipe. Before merging the two datasets, we decided to group by the recipe_id column in the interaction CSV and aggregate it with a list; this ensures that we are not losing any data by keeping the users, users' reviews, and ratings as a list per unique recipe. After merging the recipe data and the grouped by interaction data, we ended up with 83782 rows and we will primarily look at the calories which contains float values, sugar (PDV), and carbohydrates (PDV) which are both numbers as a percentage, columns to answer our question:
> Does sugary foods contain more calories than foods with more carbohydrates? 

After merging the two datasets, we changed the values in each column to be the appropriate type instead of just object type, date to pd.Datetime, and numbers to floats or ints. 

Using this analysis to describe the relationship between sugar and calories and carbs and calories allows users to see which types of foods to avoid if wanting to go on a lower calorie diet as well as even what macros to avoid. 

---
## Data Cleaning
For data cleaning, we followed the 4 steps in the write up to get basic relavant data from the two data sets. For additional cleaning, we decided to split the nutrition column into all of its macros as a seperate column for each one. This would make it easier for us to look at the sugar, carbs, and calories columns specifically. 

After splitting the nutrition columns, we changed the type of the last 7 columns to be of type float since they were all floating numbers.

We dropped the irrelavant columns such as the ratings, dates, description, and reviews as we are not using them in this data analysis.

We also added a proportion column for sugar and carbs to calories which shows the percentage daily value of those 2 macros in proportion to the number of calories of the specific recipe. 

<table border="3" class="df">
  <thead>
    <tr>
      <th>Name</th>
      <th>ID</th>
      <th>Minutes</th>
      <th>Contributor ID</th>
      <th>N Steps</th>
      <th>N Ingredients</th>
      <th>Recipe ID</th>
      <th>User ID</th>
      <th>Rating</th>
      <th>Avg Rating</th>
      <th>Calories (#)</th>
      <th>Total Fat (PDV)</th>
      <th>Sugar (PDV)</th>
      <th>Sodium (PDV)</th>
      <th>Protein (PDV)</th>
      <th>Saturated Fat (PDV)</th>
      <th>Carbohydrates (PDV)</th>
      <th>Sug > Carb</th>
      <th>Carb_Cal Proportion</th>
      <th>Sugar_Cal Proportion</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1 brownies in the world best ever</td>
      <td>333281</td>
      <td>40</td>
      <td>985201</td>
      <td>10</td>
      <td>9</td>
      <td>333281.0</td>
      <td>[386585]</td>
      <td>[4.0]</td>
      <td>4.0</td>
      <td>138.4</td>
      <td>10.0</td>
      <td>50.0</td>
      <td>3.0</td>
      <td>3.0</td>
      <td>19.0</td>
      <td>6.0</td>
      <td>True</td>
      <td>0.043353</td>
      <td>0.361272</td>
    </tr>
    <tr>
      <td>1 in canada chocolate chip cookies</td>
      <td>453467</td>
      <td>45</td>
      <td>1848091</td>
      <td>12</td>
      <td>11</td>
      <td>453467.0</td>
      <td>[424680]</td>
      <td>[5.0]</td>
      <td>5.0</td>
      <td>595.1</td>
      <td>46.0</td>
      <td>211.0</td>
      <td>22.0</td>
      <td>13.0</td>
      <td>51.0</td>
      <td>26.0</td>
      <td>True</td>
      <td>0.043690</td>
      <td>0.354562</td>
    </tr>
    <tr>
      <td>412 broccoli casserole</td>
      <td>306168</td>
      <td>40</td>
      <td>50969</td>
      <td>6</td>
      <td>9</td>
      <td>306168.0</td>
      <td>[29782, 1196280, 768828, 520830]</td>
      <td>[5.0, 5.0, 5.0, 5.0]</td>
      <td>5.0</td>
      <td>194.8</td>
      <td>20.0</td>
      <td>6.0</td>
      <td>32.0</td>
      <td>22.0</td>
      <td>36.0</td>
      <td>3.0</td>
      <td>True</td>
      <td>0.015400</td>
      <td>0.030801</td>
    </tr>
    <tr>
      <td>millionaire pound cake</td>
      <td>286009</td>
      <td>120</td>
      <td>461724</td>
      <td>7</td>
      <td>7</td>
      <td>286009.0</td>
      <td>[813055]</td>
      <td>[5.0]</td>
      <td>5.0</td>
      <td>878.3</td>
      <td>63.0</td>
      <td>326.0</td>
      <td>13.0</td>
      <td>20.0</td>
      <td>123.0</td>
      <td>39.0</td>
      <td>True</td>
      <td>0.044404</td>
      <td>0.371172</td>
    </tr>
    <tr>
      <td>2000 meatloaf</td>
      <td>475785</td>
      <td>90</td>
      <td>2202916</td>
      <td>17</td>
      <td>13</td>
      <td>475785.0</td>
      <td>[2204364, 2216720]</td>
      <td>[5.0, 5.0]</td>
      <td>5.0</td>
      <td>267.0</td>
      <td>30.0</td>
      <td>12.0</td>
      <td>12.0</td>
      <td>29.0</td>
      <td>48.0</td>
      <td>2.0</td>
      <td>True</td>
      <td>0.007491</td>
      <td>0.044944</td>
    </tr>
  </tbody>
</table>

---
## Univariate Analysis
Here we made a box plot of the distribution of sugar PDV of all recipes in the dataset. Although there are some very large values for sugar PDV, we decided to keep them in the dataset when plotting because the serving sizes of food might be large as well in proportion to sugar PDV and we don't know this just by looking at the dataset. From this plot, we can see that our min is 0, q1 is 20, median is 35, q3 is 35 with a upper fence of 132, and all values after 132 is considered an outlier. 
<iframe src="assets/sugarPDV.html" width=800 height=600 frameBorder=0></iframe>

---
## Bivariate Analysis

<iframe src="assets/sug_cal.html" width=800 height=600 frameBorder=0></iframe>