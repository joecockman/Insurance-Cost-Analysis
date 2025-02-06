# Insurance-Cost-Analysis
![The Unknown Lands](Images/medical_insurance_project.jpg)

## Project Introduction

This python project is part of the Codecademy 'Business Intelligence Data Analyst' career path I have been undertaking.

The project itself was completely open-ended. I was provided with a csv file containing medical insurance cost data and was tasked with using python to analyse the data set and draw out meaningful insights and conclusions. The csv file can be found in the file repository above.

I chose to research the following themes from the dataset:

- Average Insurance Cost by Age
- Average Insurance Cost by Gender
- Average Insurance Cost by BMI
- Average Insurance Cost by Smoking Status
- Average Insurance Cost by Region
- Smoking Prevalence by Age

I have broken these down below, showing the code I used to extract my findings and explaining the results. I have also used Excel to create graphs that display the conclusions in an easy to visualise way.

# First Steps
```
import csv
with open("insurance.csv") as insurance_csv:
    insurance_data = insurance_csv.read()
```
```
insurance_data_list = []
with open("insurance.csv") as insurance_csv:
    insurance_dict = csv.DictReader(insurance_csv, delimiter = ",")
    for row in insurance_dict:
        insurance_data_list.append(row)
```
The first step I took was importing the csv module and then opening the file as a file object named insurance_csv. I then used insurance_csv.read to view the file data in the output.

I then used the .DictReader function to create a variable called 'insurance_dict', which stored each row of the csv file as it's own dictionary. Once this was created, I used a for loop to iterate through 'insurance_dict' and add each row to a list called 'insurance_data_list'. In this way I created a list of dictionaries that I used throughout my analysis.

# Average Insurance Cost by Age
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
The first step here was to create lists that contained only the data I wanted to work with. For this question, it was 'ages' and 'charges'.

I used for loops to iterate through 'insurance_data_list' and append the 'ages' and 'charges' data to their respective lists. 'insurance_data_list' however has every value as a string value, so it was important for my analysis to make sure that both of these lists, with their values being purely numerical, were converted to either ints or floats.

Once the data was converted to a numerical type, I used the zip() function to stitch the lists together and then saved that to a list() variable called ages_and_charges_list.

I was then ready to analyse the relationship between these two points. The code I used is below.

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
```
I initialised a number of variables with values of 0, shown at the top of this code block.

I then used for loops to iterate through the 'ages_and_charges_list' and add to these predefined variables depending on the if statements.

The count variables simply add 1 in order to track the number of people in that particular group, whereas the cost variables store the sum of the cost for everyone in that group.

The count variable was important, not only because it's interesting to know how large that particular data group is, but also because I needed it to calculate the average cost.

The cost variable was divided by the count variable and rounded to two decimal places to create the 'avg' variables.

The results are shown below in a bar chart.
![Average Insurance Cost by Age](Images/age_cost_3.png)
As you can see the average cost of medical insurance increases with age throughout the age groups, however drops off at the 60+ group.



![Average Insurance Cost by Gender](Images/gender_cost.png)
![Average Insurance Cost by BMI](Images/bmi_cost_3.png)
![Average Insurance Cost by Smoking Status](Images/smoking_cost.png)
![Average Insurance Cost by Region](Images/region_cost_3.png)
![Smoking Prevalence by Age](Images/smoking_age.png)





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

This was the single largest variable in increasing insurance cost, with smokers paying almost 4x as much as non-smokers.


# Age & Cost.

# Age and Insurance Cost

## Age: 0-19:
Number of people: 137

Average Insurance Cost: $8407.35

## Age: 20-29:
Number of people: 280

Average Insurance Cost: $9561.75

## Age: 30-39:
Number of people: 257

Average Insurance Cost: $11738.78

## Age: 40-49:
Number of people: 279

Average Insurance Cost: $14399.2

## Age: 50-59:
Number of people: 271

Average Insurance Cost: $16495.23

## Age: 60+:
Number of people: 114


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
## Gender
The dataset contained 1338 records. Of these:

676 were males.

662 were females.

The average insurance cost for a male across the entire dataset was $13,390.98

The average insurance cost for a female across the entire dataset was $13,297.15

The overall insurance cost therefore was very similar for both males and females, when not specifying any other variables.

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
```
Next I looked at how a person's BMI may impact their insurance cost. Of course it's important to remember that 

## BMI: 10-20:
Number of people: 41

Average Insurance Cost: $8838.56

## BMI: 20-29:
Number of people: 631

Average Insurance Cost: $10713.67

## BMI: 30-39:
Number of people: 1247

Average Insurance Cost: $13013.97

## BMI: 40-49:
Number of people: 1335

Average Insurance Cost: $13264.21

## BMI: 50+:
Number of people: 3

Average Insurance Cost: $16034.31

# Insurance Cost & Region
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
```
```
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
## Geographical Region
The dataset was split into 4 'regions'. The distribution across those regions was mostly equal, though the price varied quite significantly, with over $1000 the difference between the cheapest region (southwest) and the most expensive (southeast). The data is shown below:

## Northeast: 
Number of records: 324

Average Insurance Cost: $13,406.38

## Northwest: 
Number of records: 325

Average Insurance Cost: $12,417.58

## Southeast: 
Number of records: 364

Average Insurance Cost: $14,735.41

## Southwest: 
Number of records: 325

Average Insurance Cost: $12,346.94

## Smokers by Age
```
below_20_count = 0
below_20_smokers = 0
below_20_non_smokers = 0

below_30_count = 0
below_30_smokers = 0
below_30_non_smokers = 0

below_40_count = 0
below_40_smokers = 0
below_40_non_smokers = 0

below_50_count = 0
below_50_smokers = 0
below_50_non_smokers = 0

below_60_count = 0
below_60_smokers = 0
below_60_non_smokers = 0

above_60_count = 0
above_60_smokers = 0
above_60_non_smokers = 0

for person in age_and_smoke_list:
    if person[0] < 20:
        below_20_count += 1
        if person[1] == "yes":
            below_20_smokers += 1
        else:
            below_20_non_smokers += 1
    if 20 <= person[0] < 30:
        below_30_count += 1
        if person[1] == "yes":
            below_30_smokers += 1
        else:
            below_30_non_smokers += 1
    if 30 <= person[0] < 40:
        below_40_count += 1
        if person[1] == "yes":
            below_40_smokers += 1
        else:
            below_40_non_smokers += 1
    if 40 <= person[0] < 50:
        below_50_count += 1
        if person[1] == "yes":
            below_50_smokers += 1
        else:
            below_50_non_smokers += 1
    if 50 <= person[0] < 60:
        below_60_count += 1
        if person[1] == "yes":
            below_60_smokers += 1
        else:
            below_60_non_smokers += 1
    if person[0] > 60:
        above_60_count += 1
        if person[1] == "yes":
            above_60_smokers += 1
        else:
            above_60_non_smokers += 1
        
below_20_percent = round(below_20_smokers / below_20_count *100, 2)
below_30_percent = round(below_30_smokers / below_30_count *100, 2)  
below_40_percent = round(below_40_smokers / below_40_count *100, 2)  
below_50_percent = round(below_50_smokers / below_50_count *100, 2)  
below_60_percent = round(below_60_smokers / below_60_count *100, 2)
above_60_percent = round(above_60_smokers / above_60_count *100, 2)  


print("Smokers by Age:")
print("-----")
print("Age: 0-19:")
print("Number of people: " + str(below_20_count))
print("Number of Smokers: " + str(below_20_smokers))
print("Number of Non-Smokers: " + str(below_20_non_smokers))
print("Smoker %: " + str(below_20_percent) + "%")
print("-----")
print("Age: 20-29:")
print("Number of people: " + str(below_30_count))
print("Number of Smokers: " + str(below_30_smokers))
print("Number of Non-Smokers: " + str(below_30_non_smokers))
print("Smoker %: " + str(below_30_percent) + "%")
print("-----")
print("Age: 30-39:")
print("Number of people: " + str(below_40_count))
print("Number of Smokers: " + str(below_40_smokers))
print("Number of Non-Smokers: " + str(below_40_non_smokers))
print("Smoker %: " + str(below_40_percent) + "%")
print("-----")
print("Age: 40-49:")
print("Number of people: " + str(below_50_count))
print("Number of Smokers: " + str(below_50_smokers))
print("Number of Non-Smokers: " + str(below_50_non_smokers))
print("Smoker %: " + str(below_50_percent) + "%")
print("-----")
print("Age: 50-59:")
print("Number of people: " + str(below_60_count))
print("Number of Smokers: " + str(below_60_smokers))
print("Number of Non-Smokers: " + str(below_60_non_smokers))
print("Smoker %: " + str(below_60_percent) + "%")
print("-----")
print("Age: 60+:")
print("Number of people: " + str(above_60_count))
print("Number of Smokers: " + str(above_60_smokers))
print("Number of Non-Smokers: " + str(above_60_non_smokers))
print("Smoker %: " + str(above_60_percent) + "%")
print("-----")
```
