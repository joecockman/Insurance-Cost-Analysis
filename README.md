# Insurance-Cost-Analysis

This python project is part of the Codecademy 'Business Intelligence Data Analyst' career path I have been undertaking.

The project itself was completely open-ended. I was provided with a csv file containing medical insurance cost data and was tasked with using python to analyse the data set and draw out meaningful insights and conclusions. The csv file can be found in the file repository above.

Below I have detailed the steps I took in approcahing and analysing the dataset, insurance.csv.


```
import csv
with open("insurance.csv") as insurance_csv:
    insurance_data = insurance_csv.read()
    print(insurance_data)
```
