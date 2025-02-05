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
The first step I took was importing the csv module and then opening the file as a file object named insurance_csv. I then used insurance_csv.read to view the file data in the output.

```
insurance_data_list = []

with open("insurance.csv") as insurance_csv:
    insurance_dict = csv.DictReader(insurance_csv, delimiter = ",")
    for row in insurance_dict:
        insurance_data_list.append(row)
print(insurance_data_list)
```

# Smoker Status & Cost.
```
smokers_cost = [person["charges"] for person in insurance_data_list if person["smoker"] == "yes"]
non_smokers_cost = [person["charges"] for person in insurance_data_list if person["smoker"] == "no"]

number_of_smokers = 0
for smoker in smokers_cost:
    number_of_smokers += 1
num_smokers = (float(number_of_smokers))

smokey_cost = []
for value in smokers_cost:
    smokey_cost.append(float(value))
smokers_total_charges = sum(smokey_cost)

number_of_non_smokers = 0
for non_smoker in non_smokers_cost:
    number_of_non_smokers += 1
num_non_smokers = (float(number_of_non_smokers))

non_smokey_cost = []
for value in non_smokers_cost:
    non_smokey_cost.append(float(value))
non_smokers_total_charges = sum(non_smokey_cost)

smokers_average_cost = smokers_total_charges / num_smokers
smokers_average_cost_rounded = round(smokers_average_cost, 2)
print("The Average cost for a smoker is: $" + str(smokers_average_cost_rounded))

non_smokers_average_cost = non_smokers_total_charges / num_non_smokers
non_smoke_rounded = round(non_smokers_average_cost, 2)
print("The Average cost for a non-smoker is: $" + str(non_smoke_rounded))
```

The Average cost for a smoker is: $32050.23
The Average cost for a non-smoker is: $8434.27


# Age & Cost.
```
ages = []
for person in insurance_data_list:
    ages.append(person["age"])

int_ages = []
for age in ages:
    int_ages.append(int(age))
```

```
charges = []
for person in insurance_data_list:
    float_charges = float(person["charges"])
    round_float_charge = round(float_charges,2)
    charges.append(round_float_charge)
print(charges)
```
```
ages_and_charges = zip(int_ages, charges)
ages_and_charges_list = list(ages_and_charges)
print(ages_and_charges_list)
```
```
below_20_cost = 0
below_20_count = 0
below_30_cost = 0
below_30_count = 0
below_40_cost = 0
below_40_count = 0
below_50_cost = 0
below_50_count = 0
below_60_cost = 0
below_60_count = 0
above_60_cost = 0
above_60_count = 0

for person in ages_and_charges_list:
    if person[0] < 20:
        below_20_cost += person[1]
        below_20_count += 1
    if 20 <= person[0] < 30:
        below_30_cost += person[1]
        below_30_count += 1
    if 30 <= person[0] < 40:
        below_40_cost += person[1]
        below_40_count += 1
    if 40 <= person[0] < 50:
        below_50_cost += person[1]
        below_50_count += 1
    if 50 <= person[0] < 60:
        below_60_cost += person[1]
        below_60_count += 1
    if person[0] >= 60:
        above_60_cost += person[1]
        above_60_count += 1

avg_below_20 = round(below_20_cost / below_20_count, 2)
avg_below_30 = round(below_30_cost / below_30_count, 2)
avg_below_40 = round(below_40_cost / below_40_count, 2)
avg_below_50 = round(below_50_cost / below_50_count, 2)
avg_below_60 = round(below_60_cost / below_60_count, 2)
avg_above_60 = round(above_60_cost / below_60_count, 2)

print("Insurance Cost by Age:")
print("-----")
print("Age: 0-19:")
print("Number of people: " + str(below_20_count))
print("Average Insurance Cost: $" + str(avg_below_20))
print("-----")
print("Age: 20-29:")
print("Number of people: " + str(below_30_count))
print("Average Insurance Cost: $" + str(avg_below_30))
print("-----")
print("Age: 30-39:")
print("Number of people: " + str(below_40_count))
print("Average Insurance Cost: $" + str(avg_below_40))
print("-----")
print("Age: 40-49:")
print("Number of people: " + str(below_50_count))
print("Average Insurance Cost: $" + str(avg_below_50))
print("-----")
print("Age: 50-59:")
print("Number of people: " + str(below_60_count))
print("Average Insurance Cost: $" + str(avg_below_60))
print("-----")
print("Age: 60+:")
print("Number of people: " + str(above_60_count))
print("Average Insurance Cost: $" + str(avg_above_60))
print("-----")
```
Insurance Cost by Age:
-----
Age: 0-19:
Number of people: 137
Average Insurance Cost: $8407.35
-----
Age: 20-29:
Number of people: 280
Average Insurance Cost: $9561.75
-----
Age: 30-39:
Number of people: 257
Average Insurance Cost: $11738.78
-----
Age: 40-49:
Number of people: 279
Average Insurance Cost: $14399.2
-----
Age: 50-59:
Number of people: 271
Average Insurance Cost: $16495.23
-----
Age: 60+:
Number of people: 114
Average Insurance Cost: $8938.28
-----

# Gender & Cost.
```
male_count = 0
males = []
female_count = 0
females = []

for person in insurance_data_list:
    if person["sex"] == "male":
        male_count += 1
        males.append(person["sex"])
    elif person["sex"] == "female":
        female_count += 1
        females.append(person["sex"])

male_charges = zip(males, charges)
female_charges = zip(females, charges)

male_cost = 0
for person in male_charges:
    male_cost += person[1]
avg_male_cost = round(male_cost / male_count,2)

female_cost = 0
for person in female_charges:
    female_cost += person[1]
avg_female_cost = round(female_cost / female_count,2)

print("Insurance Cost by Gender:")
print("-----")
print("Gender: Male")
print("Count: " + str(male_count))
print("Average Insurance Cost: $" + str(avg_male_cost))
print("-----")
print("Gender: Female")
print("Count: " + str(female_count))
print("Average Insurance Cost: $" + str(avg_female_cost))
```
Insurance Cost by Gender:
-----
Gender: Male
Count: 676
Average Insurance Cost: $13390.98
-----
Gender: Female
Count: 662
Average Insurance Cost: $13297.15
-----

# Average BMI
```
bmi = []
float_bmi = []
total_bmi = 0
for person in insurance_data_list:
    bmi.append(person["bmi"])
for value in bmi:
    value = float(value)
    float_bmi.append(value)
for value in float_bmi:
    total_bmi += value

bmi_and_charges = zip(bmi, charges)

avg_bmi = round(total_bmi / len(insurance_data_list), 2)
print("The Average BMI of individuals within the dataset is: " + str(avg_bmi))
```
```
under_20 = 0
under_20_count = 0
under_30 = 0
under_30_count = 0
under_40 = 0
under_40_count = 0
under_50 = 0
under_50_count = 0
over_50 = 0
over_50_count = 0

for person in bmi_and_charges_list:
    if person[0] < 20:
        under_20 += person[1]
        under_20_count += 1
    if person[0] < 30:
        under_30 += person[1]
        under_30_count += 1
    if person[0] < 40:
        under_40 += person[1]
        under_40_count += 1
    if person[0] < 50:
        under_50 += person[1]
        under_50_count += 1
    if person[0] > 50:
        over_50 += person[1]
        over_50_count += 1

avg_under_20 = round(under_20 / under_20_count, 2)
avg_under_30 = round(under_30 / under_30_count, 2)
avg_under_40 = round(under_40 / under_40_count, 2)
avg_under_50 = round(under_50 / under_50_count, 2)
avg_over_50 = round(over_50 / over_50_count, 2)

print("Insurance Cost by BMI:")
print("-----")
print("BMI: 10-20:")
print("Number of people: " + str(under_20_count))
print("Average Insurance Cost: $" + str(avg_under_20))
print("-----")
print("BMI: 20-29:")
print("Number of people: " + str(under_30_count))
print("Average Insurance Cost: $" + str(avg_under_30))
print("-----")
print("BMI: 30-39:")
print("Number of people: " + str(under_40_count))
print("Average Insurance Cost: $" + str(avg_under_40))
print("-----")
print("BMI: 40-49:")
print("Number of people: " + str(under_50_count))
print("Average Insurance Cost: $" + str(avg_under_50))
print("-----")
print("BMI: 50+:")
print("Number of people: " + str(over_50_count))
print("Average Insurance Cost: $" + str(avg_over_50))
print("-----")
```
Insurance Cost by BMI:
-----
BMI: 10-20:
Number of people: 41
Average Insurance Cost: $8838.56
-----
BMI: 20-29:
Number of people: 631
Average Insurance Cost: $10713.67
-----
BMI: 30-39:
Number of people: 1247
Average Insurance Cost: $13013.97
-----
BMI: 40-49:
Number of people: 1335
Average Insurance Cost: $13264.21
-----
BMI: 50+:
Number of people: 3
Average Insurance Cost: $16034.31
-----
