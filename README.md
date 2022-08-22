# Assessing Campaign Performance Using Chi Square Test For Independence

<p align="center">
  <img src="https://user-images.githubusercontent.com/69009356/185987097-b4be59cc-fa3a-41ba-a068-69aa78a17c4b.png"
 />
</p>

#Business Task
In this case we are asked by a fictious grocery company to help them to evalute the results of an A/B Test they made.
Specifically, they have emailed a group of customers with an expensive and nice designed mail advertising a new delivery service and another group with a cheaper and more standard mail, advertising the same service.
The task is to understand if there is a significant difference in terms of conversion between the two mails.

#Data
The data we are given consists of the results of the the test (converted or not) and the type of of message the customers have been exposed to. The two groups are balanced.

```python
#Importing required packages
import pandas as pd
from scipy.stats import chi2_contingency, chi2
```


```python
#Importing data
campaign_data=pd.read_excel("grocery_database.xlsx", sheet_name="campaign_data")
```


```python
#Filtering out data
campaign_data=campaign_data.loc[campaign_data["mailer_type"]!="Control"]
```


```python
campaign_data.shape[0]
```




    711




```python
observed_values=pd.crosstab(campaign_data['mailer_type'],campaign_data['signup_flag'])

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th>signup_flag</th>
      <th>0</th>
      <th>1</th>
    </tr>
    <tr>
      <th>mailer_type</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>Mailer1</th>
      <td>252</td>
      <td>123</td>
    </tr>
    <tr>
      <th>Mailer2</th>
      <td>209</td>
      <td>127</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Getting observed frequncies
observed_values=pd.crosstab(campaign_data['mailer_type'],campaign_data['signup_flag']).values
observed_values
```




    array([[252, 123],
           [209, 127]], dtype=int64)




```python
#Getting signup values
mailer1_signup_rate=123/(252+123)
mailer2_signup_rate=127/(209+127)
print(mailer1_signup_rate, mailer2_signup_rate)
```

    0.328 0.37797619047619047
    


```python
#Stating hypotesis & setting acceptance criteria
null_hypotesis="There is no relationship between mailer type and signup rate. They are independent"
alternate_hypotesis="There is a relationship between mailer type and signup rate. They are not independent"
acceptance_criteria=0.05
```


```python
#Calculating expected frequencies & Chi Square Statistic
chi2_statistic, p_value, dof,expected_values=chi2_contingency(observed_values, correction=False)
print(chi2_statistic, p_value)
```

    1.9414468614812481 0.16351152223398197
    


```python
#Finding critical value for our test
critical_value=chi2.ppf(1-acceptance_criteria, dof)
print(critical_value)
```

    3.841458820694124
    


```python
#Printing the results(Chi Square Statistic)
if chi2_statistic>=critical_value:
    print(f"As our chi square statistic of {chi2_statistic} is higher than our critical value of {critical_value}, we reject the null hypotesis and conclude that: {alternate_hypotesis}")
else:
    print(f"As our chi square statistic of {chi2_statistic} is lower than our critical value of {critical_value}, we retain the null hypotesis and conclude that: {null_hypotesis}")

```

    As our chi square statistic of 1.9414468614812481 is lower than our critical value of 3.841458820694124, we retain the null hypotesis and conclude that: There is no relationship between mailer type and signup rate. They are independent
    


```python

```

