# Property Assessment Analysis
### Description

This project delves into the concept of real-estate analytics, speicifically targeting the properties in and around Boston. By employing the data analysis techniques, the project aims in uncovering insights related to property characteristics and land value. Some of the key objectives include comparing properties based on their land value, identifying prevalent property types in the region, any specific neighborhood or street that stands out in terms of low or high property values, and mainly determining the factors that significantly influence land valuation.

### Analysis

This is broken down in 3 phases:
1. Data transformation: The schema is verified by checking whether the appropriate data types are assigned to each variables, if not then the root cause is inspected (whether it's due to the presence of characters like ',' or '.' in the data, etc). The presence of null values in data skews the analysis and may result in biases as well, these are taken care of by checking whether the complete removal of the respective field would hinder the analysis by any means. The example below is a code snip where the schema is transformed using `pyspark`.
```
#creating a function to remove the character
def remove_char(c, ch):
    return translate(c, ch, ''*len(ch))

#removing the characters from the numbers
df = df.withColumn('LAND_VALUE', remove_char(df["LAND_VALUE"], ","))

#converting the data type of the column from string to integer
df = df.withColumn('LAND_VALUE', df['LAND_VALUE'].cast(IntegerType()))
```

2. Exploratory Data Analysis: After the data is transformed, all the relevant facts and insights are gathered through visualization of the data.

<img width="327" alt="image" src="https://github.com/RonitinoR/Property-Assement-ANALYSIS/assets/126113058/9e5e8220-f44e-4bde-bd71-9604f43f2767">

The above plot indicates that over 14,000 properties were built or renovated after the year 2000. This indicates that value of the lands are increasing over time as well. 
To further investigate which neighborhood or street is expensive based on the median land values of the properties in that particular area, below plot clears the doubt.
<img width="287" alt="image" src="https://github.com/RonitinoR/Property-Assement-ANALYSIS/assets/126113058/0933fcc7-fa70-459c-991b-0a6f566bfa9e">

It clearly shows that Boston city is the most expensive area followed by Roxbury Crossing. This also further depict that the rents or leases would also be expensive if they're listed.
Further down the lane the median gross tax and land value is compared over the years to get the gauge whether there is any significant relation between them.
<img width="377" alt="image" src="https://github.com/RonitinoR/Property-Assement-ANALYSIS/assets/126113058/08de4841-aa99-4fe3-a189-b9f65690d96a">

On the basis of above visualization it is clear that there isn't any valid trends over the year, but we can definitely infer that the old properties built around 1900s have a high land value due to its historical significance.

3. Building simple regression models for further analysis.
To estimate the future values of certain important fields, a regression model is designed. Few important metrics such as Total value, Gross tax, Land value, etc are considered while building. To develop these models, the data is split into test and train sets in 3:7 ratio.
Linear Regression:
To estimate the total value based on Land SF, Number of bedrooms and year built we have used linear regression model. Based on the correlation matrix plotted above we used these fields and created a equation based on which we can predict the value of a property or flat. The results of the model are as below.
<img width="468" alt="image" src="https://github.com/RonitinoR/Property-Assement-ANALYSIS/assets/126113058/9a86fe43-0720-472b-8a57-ef2806f6a141">

The coefficients of the results can be associated with variables Land SF, No. of bedrooms and year built respectively. The intercept value is -27439978 which is like a constant in the equation. Below the intercepts we even have the results of confusion matrix to understand how much each variable is related to each other.

Logistic Regression:
This model is designed to predict if the property is owner occupied or not. Since the aim here is to predict the boolean fields (i.e., yes or no) and hence the reason logistice model is considered. In this model independent variables like living area, total value, gross tax are considered. These are the important variables by which we can predict if the property is used by the owners to live or is rented. The resulting coefficients are as follows and based on these values we can create a equation. By the RoC value which is 0.627 we can state that about 62% of data falls under the predictive model which is considered good.  
<img width="468" alt="image" src="https://github.com/RonitinoR/Property-Assement-ANALYSIS/assets/126113058/b2429bb2-d306-4851-8e07-3fda85b6c038">





