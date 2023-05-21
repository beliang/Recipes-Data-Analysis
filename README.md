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
For out bivariate analysis, we plotted the sugar PDV against the calories from a range of 0 to 2000 calories. We can interestingly see that around the 400 calorie to 600 calorie interval, there is a amount of recipes that have a very high sugar percentage daily value which is a very high sugar content for such little amount of calories. 
<iframe src="assets/sug_cal.html" width=800 height=600 frameBorder=0></iframe>

---
## Interesting Aggregates
Here is an interesting aggregtion where we took the averages of minutes, steps, ratings, and calories for how many ingredients each recipe has. Interestingly, the avg rating were equal across the board which suggests that the number of ingredients doesn't really dictate how good or bad a recipe is. However, if we look at the minutes column, we can see that there is a small gradual increase from 1 to 14-15 ingredients, and the number of ingredients after that has a huge jump of 20-30 minutes more on average. What makes even more sense is that n_steps and calories are gradually increasing which suggests that these 2 columns are related to the number of ingredients. There are some outliers in the table and this can be due to the fact that users might input the wrong number values, which may deflate or inflate the average values. 
<table border="3" class="agg">
  <thead>
    <tr>
      <th>n_ingredients</th>
      <th>minutes</th>
      <th>n_steps</th>
      <th>avg_rating</th>
      <th>calories (#)</th>
      <th>counts</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>36.714286</td>
      <td>7.571429</td>
      <td>4.861538</td>
      <td>714.650000</td>
      <td>14</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2136.453815</td>
      <td>5.931727</td>
      <td>4.692575</td>
      <td>331.983400</td>
      <td>747</td>
    </tr>
    <tr>
      <td>3</td>
      <td>335.538002</td>
      <td>5.613151</td>
      <td>4.662032</td>
      <td>306.111657</td>
      <td>2342</td>
    </tr>
    <tr>
      <td>4</td>
      <td>98.383843</td>
      <td>6.320018</td>
      <td>4.633942</td>
      <td>336.008681</td>
      <td>4481</td>
    </tr>
    <tr>
      <td>5</td>
      <td>77.129635</td>
      <td>7.125836</td>
      <td>4.647434</td>
      <td>347.801018</td>
      <td>6580</td>
    </tr>
    <tr>
      <td>6</td>
      <td>86.863238</td>
      <td>7.763025</td>
      <td>4.633105</td>
      <td>355.885221</td>
      <td>7524</td>
    </tr>
    <tr>
      <td>7</td>
      <td>77.141280</td>
      <td>8.477745</td>
      <td>4.624073</td>
      <td>391.130417</td>
      <td>8515</td>
    </tr>
    <tr>
      <td>8</td>
      <td>71.807352</td>
      <td>9.267623</td>
      <td>4.611516</td>
      <td>387.031570</td>
      <td>8923</td>
    </tr>
    <tr>
      <td>9</td>
      <td>100.003941</td>
      <td>9.907742</td>
      <td>4.606383</td>
      <td>422.504787</td>
      <td>8628</td>
    </tr>
    <tr>
      <td>10</td>
      <td>79.005228</td>
      <td>10.751400</td>
      <td>4.610229</td>
      <td>449.816183</td>
      <td>8032</td>
    </tr>
    <tr>
      <td>11</td>
      <td>79.228284</td>
      <td>11.317875</td>
      <td>4.622764</td>
      <td>467.347509</td>
      <td>6965</td>
    </tr>
    <tr>
      <td>12</td>
      <td>96.563614</td>
      <td>11.933764</td>
      <td>4.616765</td>
      <td>487.259035</td>
      <td>5722</td>
    </tr>
    <tr>
      <td>13</td>
      <td>95.228234</td>
      <td>12.752616</td>
      <td>4.631846</td>
      <td>501.750056</td>
      <td>4491</td>
    </tr>
    <tr>
      <td>14</td>
      <td>95.361472</td>
      <td>13.423933</td>
      <td>4.616374</td>
      <td>512.976871</td>
      <td>3234</td>
    </tr>
    <tr>
      <td>15</td>
      <td>104.766055</td>
      <td>14.402836</td>
      <td>4.630604</td>
      <td>558.953003</td>
      <td>2398</td>
    </tr>
    <tr>
      <td>16</td>
      <td>92.937315</td>
      <td>15.154347</td>
      <td>4.625012</td>
      <td>607.103962</td>
      <td>1691</td>
    </tr>
    <tr>
      <td>17</td>
      <td>184.643920</td>
      <td>15.794401</td>
      <td>4.632571</td>
      <td>570.566929</td>
      <td>1143</td>
    </tr>
    <tr>
      <td>18</td>
      <td>130.828829</td>
      <td>16.785071</td>
      <td>4.687617</td>
      <td>600.265380</td>
      <td>777</td>
    </tr>
    <tr>
      <td>19</td>
      <td>137.807843</td>
      <td>17.490196</td>
      <td>4.611613</td>
      <td>602.075882</td>
      <td>510</td>
    </tr>
    <tr>
      <td>20</td>
      <td>159.459318</td>
      <td>18.120735</td>
      <td>4.607544</td>
      <td>674.387402</td>
      <td>381</td>
    </tr>
    <tr>
      <td>21</td>
      <td>152.427273</td>
      <td>18.581818</td>
      <td>4.659124</td>
      <td>648.387273</td>
      <td>220</td>
    </tr>
    <tr>
      <td>22</td>
      <td>453.692308</td>
      <td>19.825175</td>
      <td>4.693353</td>
      <td>778.906294</td>
      <td>143</td>
    </tr>
    <tr>
      <td>23</td>
      <td>164.606061</td>
      <td>19.262626</td>
      <td>4.778529</td>
      <td>727.536364</td>
      <td>99</td>
    </tr>
    <tr>
      <td>24</td>
      <td>126.716216</td>
      <td>20.229730</td>
      <td>4.604672</td>
      <td>701.802703</td>
      <td>74</td>
    </tr>
    <tr>
      <td>25</td>
      <td>143.093023</td>
      <td>21.930233</td>
      <td>4.707207</td>
      <td>764.604651</td>
      <td>43</td>
    </tr>
    <tr>
      <td>26</td>
      <td>128.379310</td>
      <td>20.931034</td>
      <td>4.759298</td>
      <td>713.427586</td>
      <td>29</td>
    </tr>
    <tr>
      <td>27</td>
      <td>1086.869565</td>
      <td>26.043478</td>
      <td>4.609731</td>
      <td>1946.647826</td>
      <td>23</td>
    </tr>
    <tr>
      <td>28</td>
      <td>133.888889</td>
      <td>26.444444</td>
      <td>4.859244</td>
      <td>621.700000</td>
      <td>18</td>
    </tr>
    <tr>
      <td>29</td>
      <td>104.600000</td>
      <td>25.400000</td>
      <td>4.965714</td>
      <td>1173.330000</td>
      <td>10</td>
    </tr>
    <tr>
      <td>30</td>
      <td>127.416667</td>
      <td>23.750000</td>
      <td>4.868182</td>
      <td>655.033333</td>
      <td>12</td>
    </tr>
    <tr>
      <td>31</td>
      <td>169.375000</td>
      <td>21.000000</td>
      <td>5.000000</td>
      <td>760.687500</td>
      <td>8</td>
    </tr>
    <tr>
      <td>32</td>
      <td>55.000000</td>
      <td>34.000000</td>
      <td>5.000000</td>
      <td>697.350000</td>
      <td>2</td>
    </tr>
    <tr>
      <td>33</td>
      <td>35.000000</td>
      <td>6.000000</td>
      <td>5.000000</td>
      <td>338.200000</td>
      <td>1</td>
    </tr>
    <tr>
      <td>37</td>
      <td>240.000000</td>
      <td>6.000000</td>
      <td>5.000000</td>
      <td>10687.700000</td>
      <td>1</td>
    </tr>
  </tbody>
</table>

---
## NMAR Analysis
There are a few columns in the dataframe that have missing values, the columns are description,rating, review, and avg_rating. We believe that the description column in NMAR. We think the description column is NMAR because the person coming up with the recipe could be lazy and not include a description making it missing. The recipe could be simple enough that a description is not required.

Another column that we believe to be NMAR is the review column. We think this column is NMAR because if the recipe is bad they may not want to leave any review. They could also not leave a review because they have nothing to say about the recipe.

---
## Missingness Dependency (depend)
For one of our permutation test for missingness, we chose the 'rating' column and the 'calories (#)' column. We categorized the 'calories (#)' column into different bins depending on the calorie cutoff. We wanted to see if the missingness of 'rating' depended on the calorie cutoff. We ran a permutation with our test statistic being the absolute difference in means. From the results of the permutation test, we can see that our p-value is 0 which is less than the significance value of 0.05. This means that we reject the null, meaning that the distribution of 'calories (#)' when 'rating' is missing is not the same as the distribution of 'calories (#)' when 'rating' is not missing.

This means that the missingness in the 'rating' column is dependent on the 'calories (#)' column.



---
## Missingness Dependency (does not depend)
For one of our permutation test for missingness, we chose the 'rating' column and the date in the submitted column. We wanted to see if the missingness of 'rating' depended on the submitted column's date. We ran a permutation test with our test statistic being the absolute difference in means. From the results of the permutation test, we can see that our p-value is 0.29 which is greater than the siginficance value of 0.05. This means that we fail to reject the null, meaning that the distribution of 'submitted' when 'rating' is missing is the same as the distribution of 'submitted' when 'rating' is not missing. 

This means that the missingness in the 'rating' column is not dependent on 'submitted' date.