# Assessing Campaign Performance Using Chi Square Test For Independence

<p align="center">
  <img src="https://user-images.githubusercontent.com/69009356/185987097-b4be59cc-fa3a-41ba-a068-69aa78a17c4b.png"
 />
</p>

# Business Task
In this case we are asked by a fictious grocery company to help them to evalute the results of an A/B Test they made.
Specifically, they have emailed a group of customers with an expensive and nice designed mail advertising a new delivery service and another group with a cheaper and more standard mail, advertising the same service.
The task is to understand if there is a significant difference in terms of conversion between the two mails.

# Data
The data we are given consists of the results of the the test (converted or not) and the type of of message the customers have been exposed to. The two groups are balanced.

```python
campaign_data.head()
```
<p align="center">
  <img src="https://user-images.githubusercontent.com/69009356/185991783-af53fb31-5e64-44bf-8a23-82f6c096aa9f.JPG"
 />
</p>

# Approach
To evaluate the campaign we use the Chi Square Test For Independence
<p align="center">
χ2 = ∑(Oi – Ei)2/Ei
</p>

To do so we have to:

-Set the hypotesis and the acceptance criteria:
 - Null Hypotesis: There is no relationship between mailer type and signup rate. They are independent
 - Alternate Hypotesis: There is a relationship between mailer type and signup rate. They are not independent
 - Acceptance criteria or α: 0.05 

- Calculate the observed values:

```python
observed_values=pd.crosstab(campaign_data['mailer_type'],campaign_data['signup_flag']).values
```
<p align="center">
  <img src="[https://user-images.githubusercontent.com/69009356/185991783-af53fb31-5e64-44bf-8a23-82f6c096aa9f.JPG](https://user-images.githubusercontent.com/69009356/185993134-e87bc088-aede-4bfd-9b00-15668b45453a.JPG)"
 />
</p>

Then we proceed 
To do this in Python, we can count on the help of Scipy Package.

