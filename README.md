# Pandas Homework - Pandas, Pandas, Pandas


# Heroes of Pymoli
![Fantasy](HeroesOfPymoli/Images/Fantasy.png)

# Background
[Project Details](project_instructions_readme.md)

<div class="alert alert-block alert-info">
    <b><h1><strong>Observable Trends</strong></h1></b>
</div>

The players that purchase in game items tend to be male.  There are  **84.03%** of players purchasing in game items that are male.  This is in contrast with only **14.06%** in game purchasers being female.  Any future marketing should target males.


The age range of **20-24** outspent all other groups with 321 purchases spending a total of 973.82 dollars.  The next age range is **25-29** which purchased 155 for a total of 467.99 dollars.  And the thrid is **15-19** year olds who bought 115 items for 349.82.   These three age ranges combined account for 591 out of 780 purchase and 1791.63 of 2379.77 dollars spent.  Since this represents 75.8% of purchases and 74.7% of the dollars spent, it would make sense for any future marketing to target **15-29** years old.

**Final Critic**, **OathBreaker, Last Hope of the Breaking Storm**, and **Fiery Glass Crusider** are all in the top 5 of popular and profitable items.   It would make sense to target these three products in any future marketing.

Very few of the users make more than one in game purchase. Future marketing could target those that have made one purchase to see if they could be enticed to make additional purchases.

| # of Purchases |  # of Users |
|----------------|-------------|
|               1|          414|
|               2|          124|
|               3|           35|
|               4|            2|
|               5|            1|



# THE ANALYSIS



# Prepare the data for analysis:
```python
# Dependencies and Setup
import pandas as pd
import numpy as np
import pprint

# File to Load (Remember to Change These)
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data_df = pd.read_csv(file_to_load)
```

# Player Count
```python
# Get the length of the series created by doing a value_count on it
total_players = len(purchase_data_df["SN"].value_counts())
total_players
```




    576




```python
# Create a DataFrame to store the result and update with total_players
total_player_count = pd.DataFrame({"Total Players":[total_players]})
```

<div class="alert alert-block alert-info">
    <b><h2><strong>Player Count result</strong></h2></b>
</div>


```python
# Show the total player count
total_player_count
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>

# Purchasing Analysis (Total)
```python
# Calcualte the number of unique items
unique_items = len(purchase_data_df['Item ID'].value_counts())
unique_items
```




    179




```python
# Calculate the average price
average_price = purchase_data_df['Price'].sum() / purchase_data_df['Purchase ID'].count()
average_price
```




    3.0509871794871795




```python
# Calculate the total number of purchases
number_purchases = purchase_data_df['Purchase ID'].count()
number_purchases
```




    780




```python
# Calculate total revenue for all purchases
total_revenue = purchase_data_df['Price'].sum()
total_revenue
```




    2379.77




```python
# Create a dataframe with all of our summary information
purchasing_totals_df = pd.DataFrame({"Number of Unique Items":[unique_items],
                                    "Average Price":[average_price],
                                    "Number of Purchases":[number_purchases],
                                    "Total Revenue":[total_revenue]  
                                    },)
purchasing_totals_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>179</td>
      <td>3.050987</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting for the currancy data in 'Average Price' and 'Total Revenue'
purchasing_totals_df["Average Price"] = purchasing_totals_df["Average Price"].map("${:,.2f}".format)
purchasing_totals_df["Total Revenue"] = purchasing_totals_df["Total Revenue"].map("${:,.2f}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Purchasing Analysis (Total) result</strong></h2></b>
</div>


```python
# Show the Purchasing Analysis (Total) information
purchasing_totals_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price</th>
      <th>Number of Purchases</th>
      <th>Total Revenue</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>179</td>
      <td>$3.05</td>
      <td>780</td>
      <td>$2,379.77</td>
    </tr>
  </tbody>
</table>
</div>


# Gender Demographics

```python
# Group purchase_data by Gender
grouped_gender_df = purchase_data_df.groupby("Gender")
```


```python
# Count the total of screen names "SN" by gender
total_sn_by_gender = grouped_gender_df.nunique()["SN"]
total_sn_by_gender
```




    Gender
    Female                    81
    Male                     484
    Other / Non-Disclosed     11
    Name: SN, dtype: int64




```python
# Calculate the percentage of players for each gender
percentage_of_players = total_sn_by_gender / total_players
percentage_of_players
```




    Gender
    Female                   0.140625
    Male                     0.840278
    Other / Non-Disclosed    0.019097
    Name: SN, dtype: float64




```python
# Create a dataframe to store our totals
gender_percent_summary_df = pd.DataFrame({"Total Count": total_sn_by_gender,"Percentage of Players": percentage_of_players})
gender_percent_summary_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Female</td>
      <td>81</td>
      <td>0.140625</td>
    </tr>
    <tr>
      <td>Male</td>
      <td>484</td>
      <td>0.840278</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>0.019097</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Sort the data by Total Count
sorted_gender_percent_summary_df = gender_percent_summary_df.sort_values('Total Count',ascending=False)
sorted_gender_percent_summary_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Male</td>
      <td>484</td>
      <td>0.840278</td>
    </tr>
    <tr>
      <td>Female</td>
      <td>81</td>
      <td>0.140625</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>0.019097</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting to the Percentage of Players data
sorted_gender_percent_summary_df["Percentage of Players"] = sorted_gender_percent_summary_df["Percentage of Players"].map("{:.2%}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Gender Demographics result</strong></h2></b>
</div>


```python
# Show the Gender Demographics information
sorted_gender_percent_summary_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Male</td>
      <td>484</td>
      <td>84.03%</td>
    </tr>
    <tr>
      <td>Female</td>
      <td>81</td>
      <td>14.06%</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>1.91%</td>
    </tr>
  </tbody>
</table>
</div>



# Purchasing Analysis (Gender)

```python
# Calculate the number of purchases per Gender
gender_number_purchases = grouped_gender_df['Purchase ID'].count()
gender_number_purchases
```




    Gender
    Female                   113
    Male                     652
    Other / Non-Disclosed     15
    Name: Purchase ID, dtype: int64




```python
# Calculate the average price per Gender
gender_average_price = grouped_gender_df['Price'].sum() / grouped_gender_df['Purchase ID'].count()
gender_average_price
```




    Gender
    Female                   3.203009
    Male                     3.017853
    Other / Non-Disclosed    3.346000
    dtype: float64




```python
# Calculate the total revenue per Gender
gender_total_revenue = grouped_gender_df['Price'].sum()
gender_total_revenue
```




    Gender
    Female                    361.94
    Male                     1967.64
    Other / Non-Disclosed      50.19
    Name: Price, dtype: float64




```python
# Group purchase_data by SN and by Gender in order to calculate the average purchase per person
grouped_sn_gender_df = purchase_data_df.groupby(["SN","Gender"])
grouped_sn_gender_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>775</td>
      <td>775</td>
      <td>Aethedru70</td>
      <td>21</td>
      <td>Female</td>
      <td>60</td>
      <td>Wolf</td>
      <td>3.54</td>
    </tr>
    <tr>
      <td>776</td>
      <td>776</td>
      <td>Iral74</td>
      <td>21</td>
      <td>Male</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.63</td>
    </tr>
    <tr>
      <td>777</td>
      <td>777</td>
      <td>Yathecal72</td>
      <td>20</td>
      <td>Male</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>3.46</td>
    </tr>
    <tr>
      <td>778</td>
      <td>778</td>
      <td>Sisur91</td>
      <td>7</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.19</td>
    </tr>
    <tr>
      <td>779</td>
      <td>779</td>
      <td>Ennrian78</td>
      <td>24</td>
      <td>Male</td>
      <td>50</td>
      <td>Dawn</td>
      <td>4.60</td>
    </tr>
  </tbody>
</table>
<p>780 rows × 7 columns</p>
</div>




```python
# Calculate the total purchase per SN and Gender
total_purchase_gender_by_sn = grouped_sn_gender_df['Price'].sum()
total_purchase_gender_by_sn
```




    SN             Gender
    Adairialis76   Male      2.28
    Adastirin33    Female    4.48
    Aeda94         Male      4.91
    Aela59         Male      4.32
    Aelaria33      Male      1.79
                             ... 
    Yathecal82     Female    6.22
    Yathedeu43     Male      6.02
    Yoishirrala98  Female    4.58
    Zhisrisu83     Male      7.89
    Zontibe81      Male      8.03
    Name: Price, Length: 576, dtype: float64




```python
# Now group by Gender calculate the averge purchase per person by Gender
average_total_purchase_by_gender = total_purchase_gender_by_sn.groupby('Gender').mean()
average_total_purchase_by_gender
```




    Gender
    Female                   4.468395
    Male                     4.065372
    Other / Non-Disclosed    4.562727
    Name: Price, dtype: float64




```python
# Add the data into the summary DataFram3e
purchasing_analysis_gender_df = pd.DataFrame({"Purchase Count": gender_number_purchases,
                                              "Average Purchase Price": gender_average_price,
                                              "Total Purchase Value": gender_total_revenue,
                                             "Average Total Purchase Per Person": average_total_purchase_by_gender
                                            })
purchasing_analysis_gender_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Average Total Purchase Per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Female</td>
      <td>113</td>
      <td>3.203009</td>
      <td>361.94</td>
      <td>4.468395</td>
    </tr>
    <tr>
      <td>Male</td>
      <td>652</td>
      <td>3.017853</td>
      <td>1967.64</td>
      <td>4.065372</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>15</td>
      <td>3.346000</td>
      <td>50.19</td>
      <td>4.562727</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting to the 3 currency columns of data
purchasing_analysis_gender_df["Average Purchase Price"] = purchasing_analysis_gender_df["Average Purchase Price"].map("${:,.2f}".format)
purchasing_analysis_gender_df["Total Purchase Value"] = purchasing_analysis_gender_df["Total Purchase Value"].map("${:,.2f}".format)
purchasing_analysis_gender_df["Average Total Purchase Per Person"] = purchasing_analysis_gender_df["Average Total Purchase Per Person"].map("${:,.2f}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Purchasing Analysis (Gender) result</strong></h2></b>
</div>


```python
# Show the Purchasing Analysis (Gender) information
purchasing_analysis_gender_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Average Total Purchase Per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Female</td>
      <td>113</td>
      <td>$3.20</td>
      <td>$361.94</td>
      <td>$4.47</td>
    </tr>
    <tr>
      <td>Male</td>
      <td>652</td>
      <td>$3.02</td>
      <td>$1,967.64</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>15</td>
      <td>$3.35</td>
      <td>$50.19</td>
      <td>$4.56</td>
    </tr>
  </tbody>
</table>
</div>

# Age Demographics

```python
# Create bins in which to place values based upon age
bins = [0, 9.9, 13.9, 18.9, 23.9, 28.9, 33.9, 38.9, 125]

# Create labels for these bins
group_labels = ["  <10", "10-14", "15-19", "20-24", "25-29", "30-34",
                "35_39", "  40+"]
```


```python
# Slice the data and place it into bins
purchase_data_df['Age Ranges'] = pd.cut(purchase_data_df["Age"],bins,labels=group_labels,include_lowest=True)
purchase_data_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Age Ranges</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
      <td>25-29</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
      <td>25-29</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>775</td>
      <td>775</td>
      <td>Aethedru70</td>
      <td>21</td>
      <td>Female</td>
      <td>60</td>
      <td>Wolf</td>
      <td>3.54</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>776</td>
      <td>776</td>
      <td>Iral74</td>
      <td>21</td>
      <td>Male</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.63</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>777</td>
      <td>777</td>
      <td>Yathecal72</td>
      <td>20</td>
      <td>Male</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>3.46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>778</td>
      <td>778</td>
      <td>Sisur91</td>
      <td>7</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.19</td>
      <td>&lt;10</td>
    </tr>
    <tr>
      <td>779</td>
      <td>779</td>
      <td>Ennrian78</td>
      <td>24</td>
      <td>Male</td>
      <td>50</td>
      <td>Dawn</td>
      <td>4.60</td>
      <td>25-29</td>
    </tr>
  </tbody>
</table>
<p>780 rows × 8 columns</p>
</div>




```python
# Group the data by 'Age Ranges'
grouped_age_ranges_df = purchase_data_df.groupby('Age Ranges')
```


```python
# Count the total of screen names "SN" by age group
total_sn_by_age_ranges = grouped_age_ranges_df["SN"].nunique()
total_sn_by_age_ranges
```




    Age Ranges
      <10     17
    10-14     20
    15-19     92
    20-24    227
    25-29    115
    30-34     55
    35_39     32
      40+     18
    Name: SN, dtype: int64




```python
# # Total count by gender and divivde by total players 
percentage_of_players_by_age_ranges = total_sn_by_age_ranges / total_players
percentage_of_players_by_age_ranges
```




    Age Ranges
      <10    0.029514
    10-14    0.034722
    15-19    0.159722
    20-24    0.394097
    25-29    0.199653
    30-34    0.095486
    35_39    0.055556
      40+    0.031250
    Name: SN, dtype: float64




```python
# Add the data into the summary DataFrame
age_range_percent_summary_df = pd.DataFrame({"Total Count": total_sn_by_age_ranges,"Percentage of Players": percentage_of_players_by_age_ranges})
age_range_percent_summary_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Ranges</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;10</td>
      <td>17</td>
      <td>0.029514</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>20</td>
      <td>0.034722</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>92</td>
      <td>0.159722</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>227</td>
      <td>0.394097</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>115</td>
      <td>0.199653</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>55</td>
      <td>0.095486</td>
    </tr>
    <tr>
      <td>35_39</td>
      <td>32</td>
      <td>0.055556</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>18</td>
      <td>0.031250</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add percentage formatting to the 'Percentage of Players' data
age_range_percent_summary_df["Percentage of Players"] = age_range_percent_summary_df["Percentage of Players"].map("{:.2%}".format)
```

<div class="alert alert-block alert-info">
    <b><h2><strong>Age Demographics result</strong></h2></b>
</div>


```python
# Show the Age Demographics information
age_range_percent_summary_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Count</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age Ranges</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;10</td>
      <td>17</td>
      <td>2.95%</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>20</td>
      <td>3.47%</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>92</td>
      <td>15.97%</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>227</td>
      <td>39.41%</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>115</td>
      <td>19.97%</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>55</td>
      <td>9.55%</td>
    </tr>
    <tr>
      <td>35_39</td>
      <td>32</td>
      <td>5.56%</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>18</td>
      <td>3.12%</td>
    </tr>
  </tbody>
</table>
</div>

# Purchasing Analysis (Age)


```python
# Calculate the number of purchase per 'Age Range'
age_ranges_number_purchases = grouped_age_ranges_df['Purchase ID'].count()
age_ranges_number_purchases
```




    Age Ranges
      <10     23
    10-14     26
    15-19    115
    20-24    321
    25-29    155
    30-34     77
    35_39     44
      40+     19
    Name: Purchase ID, dtype: int64




```python
# Calculate the average price per 'Age Range'
age_ranges_average_price = grouped_age_ranges_df['Price'].sum() / grouped_age_ranges_df['Purchase ID'].count()
age_ranges_average_price
```




    Age Ranges
      <10    3.353478
    10-14    2.918077
    15-19    3.041913
    20-24    3.033707
    25-29    3.019290
    30-34    2.949351
    35_39    3.329091
      40+    3.240000
    dtype: float64




```python
# Calculate the total revenue per 'Age Range'
age_ranges_total_revenue = grouped_age_ranges_df['Price'].sum()
age_ranges_total_revenue
```




    Age Ranges
      <10     77.13
    10-14     75.87
    15-19    349.82
    20-24    973.82
    25-29    467.99
    30-34    227.10
    35_39    146.48
      40+     61.56
    Name: Price, dtype: float64




```python
# Group purchase_data by Gender
grouped_sn_age_ranges_df = purchase_data_df.groupby(["SN","Age Ranges"])
grouped_sn_age_ranges_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Age Ranges</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
      <td>25-29</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
      <td>25-29</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>775</td>
      <td>775</td>
      <td>Aethedru70</td>
      <td>21</td>
      <td>Female</td>
      <td>60</td>
      <td>Wolf</td>
      <td>3.54</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>776</td>
      <td>776</td>
      <td>Iral74</td>
      <td>21</td>
      <td>Male</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.63</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>777</td>
      <td>777</td>
      <td>Yathecal72</td>
      <td>20</td>
      <td>Male</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>3.46</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>778</td>
      <td>778</td>
      <td>Sisur91</td>
      <td>7</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.19</td>
      <td>&lt;10</td>
    </tr>
    <tr>
      <td>779</td>
      <td>779</td>
      <td>Ennrian78</td>
      <td>24</td>
      <td>Male</td>
      <td>50</td>
      <td>Dawn</td>
      <td>4.60</td>
      <td>25-29</td>
    </tr>
  </tbody>
</table>
<p>780 rows × 8 columns</p>
</div>




```python
# Calculate the total purchases by 'Age Range'
total_purchase_age_ranges_by_sn = grouped_sn_age_ranges_df['Price'].sum()
total_purchase_age_ranges_by_sn
```




    SN            Age Ranges
    Adairialis76    <10          NaN
                  10-14          NaN
                  15-19         2.28
                  20-24          NaN
                  25-29          NaN
                                ... 
    Zontibe81     20-24         8.03
                  25-29          NaN
                  30-34          NaN
                  35_39          NaN
                    40+          NaN
    Name: Price, Length: 4608, dtype: float64




```python
# Calculate the average total purchase for each age range
average_total_purchase_by_age_ranges = total_purchase_age_ranges_by_sn.groupby('Age Ranges').mean()
average_total_purchase_by_age_ranges
```




    Age Ranges
      <10    4.537059
    10-14    3.793500
    15-19    3.802391
    20-24    4.289956
    25-29    4.069478
    30-34    4.129091
    35_39    4.577500
      40+    3.420000
    Name: Price, dtype: float64




```python
# Add the data into the summary DataFram3e
purchasing_analysis_age_ranges_df = pd.DataFrame({"Purchase Count": age_ranges_number_purchases,
                                              "Average Purchase Price": age_ranges_average_price,
                                              "Total Purchase Value": age_ranges_total_revenue,
                                             "Average Total Purchase Per Person": average_total_purchase_by_age_ranges
                                            })
purchasing_analysis_age_ranges_df
```




<div>
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Average Total Purchase Per Person</th>
    </tr>
    <tr>
      <th>Age Ranges</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;10</td>
      <td>23</td>
      <td>3.353478</td>
      <td>77.13</td>
      <td>4.537059</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>26</td>
      <td>2.918077</td>
      <td>75.87</td>
      <td>3.793500</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>115</td>
      <td>3.041913</td>
      <td>349.82</td>
      <td>3.802391</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>321</td>
      <td>3.033707</td>
      <td>973.82</td>
      <td>4.289956</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>155</td>
      <td>3.019290</td>
      <td>467.99</td>
      <td>4.069478</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>77</td>
      <td>2.949351</td>
      <td>227.10</td>
      <td>4.129091</td>
    </tr>
    <tr>
      <td>35_39</td>
      <td>44</td>
      <td>3.329091</td>
      <td>146.48</td>
      <td>4.577500</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>19</td>
      <td>3.240000</td>
      <td>61.56</td>
      <td>3.420000</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting to the 3 currency fields of data
purchasing_analysis_age_ranges_df["Average Purchase Price"] = purchasing_analysis_age_ranges_df["Average Purchase Price"].map("${:,.2f}".format)
purchasing_analysis_age_ranges_df["Total Purchase Value"] = purchasing_analysis_age_ranges_df["Total Purchase Value"].map("${:,.2f}".format)
purchasing_analysis_age_ranges_df["Average Total Purchase Per Person"] = purchasing_analysis_age_ranges_df["Average Total Purchase Per Person"].map("${:,.2f}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Purchasing Analysis (Age) result</strong></h2></b>
</div>


```python
# Show the Purchasing Analysis (Age) information
purchasing_analysis_age_ranges_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Average Total Purchase Per Person</th>
    </tr>
    <tr>
      <th>Age Ranges</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;10</td>
      <td>23</td>
      <td>$3.35</td>
      <td>$77.13</td>
      <td>$4.54</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>26</td>
      <td>$2.92</td>
      <td>$75.87</td>
      <td>$3.79</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>115</td>
      <td>$3.04</td>
      <td>$349.82</td>
      <td>$3.80</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>321</td>
      <td>$3.03</td>
      <td>$973.82</td>
      <td>$4.29</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>155</td>
      <td>$3.02</td>
      <td>$467.99</td>
      <td>$4.07</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>77</td>
      <td>$2.95</td>
      <td>$227.10</td>
      <td>$4.13</td>
    </tr>
    <tr>
      <td>35_39</td>
      <td>44</td>
      <td>$3.33</td>
      <td>$146.48</td>
      <td>$4.58</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>19</td>
      <td>$3.24</td>
      <td>$61.56</td>
      <td>$3.42</td>
    </tr>
  </tbody>
</table>
</div>

# Top Spenders


```python
# Group the purchase data by screen name ('SN')
grouped_by_sn_df = purchase_data_df.groupby('SN')
```


```python
# Calculate the number of purchase for each user
sn_number_purchases = grouped_by_sn_df['Purchase ID'].count()
sn_number_purchases
```




    SN
    Adairialis76     1
    Adastirin33      1
    Aeda94           1
    Aela59           1
    Aelaria33        1
                    ..
    Yathecal82       3
    Yathedeu43       2
    Yoishirrala98    1
    Zhisrisu83       2
    Zontibe81        3
    Name: Purchase ID, Length: 576, dtype: int64




```python
# Calculate how many users had made 1 - 5 purchases
sn_number_purchases.value_counts()
```




    1    414
    2    124
    3     35
    4      2
    5      1
    Name: Purchase ID, dtype: int64




```python
# Calculate the average price paid per user
sn_average_price = grouped_by_sn_df['Price'].sum() / grouped_by_sn_df['Purchase ID'].count()
sn_average_price
```




    SN
    Adairialis76     2.280000
    Adastirin33      4.480000
    Aeda94           4.910000
    Aela59           4.320000
    Aelaria33        1.790000
                       ...   
    Yathecal82       2.073333
    Yathedeu43       3.010000
    Yoishirrala98    4.580000
    Zhisrisu83       3.945000
    Zontibe81        2.676667
    Length: 576, dtype: float64




```python
# Calculate the total purchase amount made by each user
sn_total_revenue = grouped_by_sn_df['Price'].sum()
sn_total_revenue
```




    SN
    Adairialis76     2.28
    Adastirin33      4.48
    Aeda94           4.91
    Aela59           4.32
    Aelaria33        1.79
                     ... 
    Yathecal82       6.22
    Yathedeu43       6.02
    Yoishirrala98    4.58
    Zhisrisu83       7.89
    Zontibe81        8.03
    Name: Price, Length: 576, dtype: float64




```python
# Add the data into the summary DataFram3e
top_spenders_df = pd.DataFrame({"Purchase Count": sn_number_purchases,
                                              "Average Purchase Price": sn_average_price,
                                              "Total Purchase Value": sn_total_revenue,
                                            })
top_spenders_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Adairialis76</td>
      <td>1</td>
      <td>2.280000</td>
      <td>2.28</td>
    </tr>
    <tr>
      <td>Adastirin33</td>
      <td>1</td>
      <td>4.480000</td>
      <td>4.48</td>
    </tr>
    <tr>
      <td>Aeda94</td>
      <td>1</td>
      <td>4.910000</td>
      <td>4.91</td>
    </tr>
    <tr>
      <td>Aela59</td>
      <td>1</td>
      <td>4.320000</td>
      <td>4.32</td>
    </tr>
    <tr>
      <td>Aelaria33</td>
      <td>1</td>
      <td>1.790000</td>
      <td>1.79</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>Yathecal82</td>
      <td>3</td>
      <td>2.073333</td>
      <td>6.22</td>
    </tr>
    <tr>
      <td>Yathedeu43</td>
      <td>2</td>
      <td>3.010000</td>
      <td>6.02</td>
    </tr>
    <tr>
      <td>Yoishirrala98</td>
      <td>1</td>
      <td>4.580000</td>
      <td>4.58</td>
    </tr>
    <tr>
      <td>Zhisrisu83</td>
      <td>2</td>
      <td>3.945000</td>
      <td>7.89</td>
    </tr>
    <tr>
      <td>Zontibe81</td>
      <td>3</td>
      <td>2.676667</td>
      <td>8.03</td>
    </tr>
  </tbody>
</table>
<p>576 rows × 3 columns</p>
</div>




```python
# Sort the data by Total Count
sorted_top_speners_df = top_spenders_df.sort_values('Total Purchase Value',ascending=False)
sorted_top_speners_df.head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lisosia93</td>
      <td>5</td>
      <td>3.792000</td>
      <td>18.96</td>
    </tr>
    <tr>
      <td>Idastidru52</td>
      <td>4</td>
      <td>3.862500</td>
      <td>15.45</td>
    </tr>
    <tr>
      <td>Chamjask73</td>
      <td>3</td>
      <td>4.610000</td>
      <td>13.83</td>
    </tr>
    <tr>
      <td>Iral74</td>
      <td>4</td>
      <td>3.405000</td>
      <td>13.62</td>
    </tr>
    <tr>
      <td>Iskadarya95</td>
      <td>3</td>
      <td>4.366667</td>
      <td>13.10</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting to the two currency columns
sorted_top_speners_df["Average Purchase Price"] = sorted_top_speners_df["Average Purchase Price"].map("${:,.2f}".format)
sorted_top_speners_df["Total Purchase Value"] = sorted_top_speners_df["Total Purchase Value"].map("${:,.2f}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Top Spenders result</strong></h2></b>
</div>


```python
# Show the Top Spenders
sorted_top_speners_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>SN</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lisosia93</td>
      <td>5</td>
      <td>$3.79</td>
      <td>$18.96</td>
    </tr>
    <tr>
      <td>Idastidru52</td>
      <td>4</td>
      <td>$3.86</td>
      <td>$15.45</td>
    </tr>
    <tr>
      <td>Chamjask73</td>
      <td>3</td>
      <td>$4.61</td>
      <td>$13.83</td>
    </tr>
    <tr>
      <td>Iral74</td>
      <td>4</td>
      <td>$3.40</td>
      <td>$13.62</td>
    </tr>
    <tr>
      <td>Iskadarya95</td>
      <td>3</td>
      <td>$4.37</td>
      <td>$13.10</td>
    </tr>
  </tbody>
</table>
</div>


# Most Popular Items

```python
# Create a dataframe of the 'Item ID', 'Item Name', and 'Price'
items_df = purchase_data_df[['Item ID','Item Name','Price']]
items_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <td>1</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <td>2</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <td>3</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <td>4</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>775</td>
      <td>60</td>
      <td>Wolf</td>
      <td>3.54</td>
    </tr>
    <tr>
      <td>776</td>
      <td>164</td>
      <td>Exiled Doomblade</td>
      <td>1.63</td>
    </tr>
    <tr>
      <td>777</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>3.46</td>
    </tr>
    <tr>
      <td>778</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.19</td>
    </tr>
    <tr>
      <td>779</td>
      <td>50</td>
      <td>Dawn</td>
      <td>4.60</td>
    </tr>
  </tbody>
</table>
<p>780 rows × 3 columns</p>
</div>




```python
# Group the data by 'Item ID' and 'Item Name'
grouped_items_df = items_df.groupby(['Item ID','Item Name'])
grouped_items_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <td>1</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <td>2</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <td>3</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <td>4</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>764</td>
      <td>113</td>
      <td>Solitude's Reaver</td>
      <td>4.07</td>
    </tr>
    <tr>
      <td>765</td>
      <td>130</td>
      <td>Alpha</td>
      <td>2.07</td>
    </tr>
    <tr>
      <td>766</td>
      <td>58</td>
      <td>Freak's Bite, Favor of Holy Might</td>
      <td>4.14</td>
    </tr>
    <tr>
      <td>777</td>
      <td>67</td>
      <td>Celeste, Incarnation of the Corrupted</td>
      <td>3.46</td>
    </tr>
    <tr>
      <td>779</td>
      <td>50</td>
      <td>Dawn</td>
      <td>4.60</td>
    </tr>
  </tbody>
</table>
<p>690 rows × 3 columns</p>
</div>




```python
# Count the number of purchase for each item
item_number_purchases = grouped_items_df['Item ID'].count()
item_number_purchases
```




    Item ID  Item Name                                   
    0        Splinter                                         4
    1        Crucifer                                         4
    2        Verdict                                          6
    3        Phantomlight                                     6
    4        Bloodlord's Fetish                               5
                                                             ..
    178      Oathbreaker, Last Hope of the Breaking Storm    12
    179      Wolf, Promise of the Moonwalker                  6
    181      Reaper's Toll                                    5
    182      Toothpick                                        3
    183      Dragon's Greatsword                              3
    Name: Item ID, Length: 179, dtype: int64




```python
# Calculate the total money paid for each item
item_total_revenue = grouped_items_df['Price'].sum()
item_total_revenue
```




    Item ID  Item Name                                   
    0        Splinter                                         5.12
    1        Crucifer                                        11.77
    2        Verdict                                         14.88
    3        Phantomlight                                    14.94
    4        Bloodlord's Fetish                               8.50
                                                             ...  
    178      Oathbreaker, Last Hope of the Breaking Storm    50.76
    179      Wolf, Promise of the Moonwalker                 26.88
    181      Reaper's Toll                                    8.30
    182      Toothpick                                       12.09
    183      Dragon's Greatsword                              3.27
    Name: Price, Length: 179, dtype: float64




```python
# Calculate the item price
item_price = item_total_revenue / item_number_purchases
item_price
```




    Item ID  Item Name                                   
    0        Splinter                                        1.2800
    1        Crucifer                                        2.9425
    2        Verdict                                         2.4800
    3        Phantomlight                                    2.4900
    4        Bloodlord's Fetish                              1.7000
                                                              ...  
    178      Oathbreaker, Last Hope of the Breaking Storm    4.2300
    179      Wolf, Promise of the Moonwalker                 4.4800
    181      Reaper's Toll                                   1.6600
    182      Toothpick                                       4.0300
    183      Dragon's Greatsword                             1.0900
    Length: 179, dtype: float64




```python
# Add the data into the summary DataFrame for Most Popular Items
most_popular_df = pd.DataFrame({"Purchase Count": item_number_purchases,
                                "Item Price": item_price,
                                "Total Purchase Value": item_total_revenue,
                              })
most_popular_df
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>Splinter</td>
      <td>4</td>
      <td>1.2800</td>
      <td>5.12</td>
    </tr>
    <tr>
      <td>1</td>
      <td>Crucifer</td>
      <td>4</td>
      <td>2.9425</td>
      <td>11.77</td>
    </tr>
    <tr>
      <td>2</td>
      <td>Verdict</td>
      <td>6</td>
      <td>2.4800</td>
      <td>14.88</td>
    </tr>
    <tr>
      <td>3</td>
      <td>Phantomlight</td>
      <td>6</td>
      <td>2.4900</td>
      <td>14.94</td>
    </tr>
    <tr>
      <td>4</td>
      <td>Bloodlord's Fetish</td>
      <td>5</td>
      <td>1.7000</td>
      <td>8.50</td>
    </tr>
    <tr>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.2300</td>
      <td>50.76</td>
    </tr>
    <tr>
      <td>179</td>
      <td>Wolf, Promise of the Moonwalker</td>
      <td>6</td>
      <td>4.4800</td>
      <td>26.88</td>
    </tr>
    <tr>
      <td>181</td>
      <td>Reaper's Toll</td>
      <td>5</td>
      <td>1.6600</td>
      <td>8.30</td>
    </tr>
    <tr>
      <td>182</td>
      <td>Toothpick</td>
      <td>3</td>
      <td>4.0300</td>
      <td>12.09</td>
    </tr>
    <tr>
      <td>183</td>
      <td>Dragon's Greatsword</td>
      <td>3</td>
      <td>1.0900</td>
      <td>3.27</td>
    </tr>
  </tbody>
</table>
<p>179 rows × 3 columns</p>
</div>




```python
# Sort the data by Total Count
sorted_most_popular_df = most_popular_df.sort_values('Purchase Count',ascending=False)
sorted_most_popular_df.head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>92</td>
      <td>Final Critic</td>
      <td>13</td>
      <td>4.614615</td>
      <td>59.99</td>
    </tr>
    <tr>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.230000</td>
      <td>50.76</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.580000</td>
      <td>41.22</td>
    </tr>
    <tr>
      <td>132</td>
      <td>Persuasion</td>
      <td>9</td>
      <td>3.221111</td>
      <td>28.99</td>
    </tr>
    <tr>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>3.530000</td>
      <td>31.77</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting for the two currency columns
sorted_most_popular_df["Item Price"] = sorted_most_popular_df["Item Price"].map("${:,.2f}".format)
sorted_most_popular_df["Total Purchase Value"] = sorted_most_popular_df["Total Purchase Value"].map("${:,.2f}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Most Popular Items result</strong></h2></b>
</div>


```python
# Show the Five Most Popular Items
sorted_most_popular_df.head()
```




<div>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>92</td>
      <td>Final Critic</td>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <td>132</td>
      <td>Persuasion</td>
      <td>9</td>
      <td>$3.22</td>
      <td>$28.99</td>
    </tr>
    <tr>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>$3.53</td>
      <td>$31.77</td>
    </tr>
  </tbody>
</table>
</div>


# Most Profitable Items


```python
# Sort the data by Total Count
sorted_most_profitable_df = most_popular_df.sort_values('Total Purchase Value',ascending=False)
sorted_most_profitable_df.head(5)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>92</td>
      <td>Final Critic</td>
      <td>13</td>
      <td>4.614615</td>
      <td>59.99</td>
    </tr>
    <tr>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.230000</td>
      <td>50.76</td>
    </tr>
    <tr>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.900000</td>
      <td>44.10</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.580000</td>
      <td>41.22</td>
    </tr>
    <tr>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>8</td>
      <td>4.350000</td>
      <td>34.80</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Add formatting to our table for the Item Price and Total Purchase Value
sorted_most_profitable_df["Item Price"] = sorted_most_profitable_df["Item Price"].map("${:,.2f}".format)
sorted_most_profitable_df["Total Purchase Value"] = sorted_most_profitable_df["Total Purchase Value"].map("${:,.2f}".format)

```

<div class="alert alert-block alert-info">
    <b><h2><strong>Most Profitable Items result</strong></h2></b>
</div>


```python
# Show the Five Most Profitable Items
sorted_most_profitable_df.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>92</td>
      <td>Final Critic</td>
      <td>13</td>
      <td>$4.61</td>
      <td>$59.99</td>
    </tr>
    <tr>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>$4.23</td>
      <td>$50.76</td>
    </tr>
    <tr>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>$4.90</td>
      <td>$44.10</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>$4.58</td>
      <td>$41.22</td>
    </tr>
    <tr>
      <td>103</td>
      <td>Singed Scalpel</td>
      <td>8</td>
      <td>$4.35</td>
      <td>$34.80</td>
    </tr>
  </tbody>
</table>
</div>
