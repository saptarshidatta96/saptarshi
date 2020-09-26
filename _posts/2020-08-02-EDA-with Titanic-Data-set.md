---
layout: post
title: EDA with Titanic Dataset - Literature
published: true
---
The Titanic data set is a famous data set that beginners in Machine Learning always refer to. However, the data set presents some interesting EDA opportunities which can be applied towards further complex problems.

# Problem Description

The sinking of the Titanic is one of the most infamous shipwrecks in history.

On April 15, 1912, during her maiden voyage, the widely considered “unsinkable” RMS Titanic sank after colliding with an iceberg. Unfortunately, there weren’t enough lifeboats for everyone onboard, resulting in the death of 1502 out of 2224 passengers and crew.

While there was some element of luck involved in surviving, it seems some groups of people were more likely to survive than others.

In this challenge, we ask you to build a predictive model that answers the question: “what sorts of people were more likely to survive?” using passenger data (ie name, age, gender, socio-economic class, etc).

# Data Dictionary:
![]({{site.baseurl}}/_posts/data%20dictionary.JPG)

# Assumptions:

The following has been assumed with respect to some of the variables and further has been used to derive some additional variables for better analysis.

pclass: This variable is a proxy for socio-economic status (SES)

- 1st = Upper

- 2nd = Middle

- 3rd = Lower

age: This variable provides information about the age of the passenger

- Age is fractional if less than 1.

- If the age is estimated, is it in the form of xx.5

sibsp: The variable defines family relations in this way...

- Sibling = brother, sister, stepbrother, stepsister

- Spouse = husband, wife (mistresses and fiances have been ignored)

parch: This variable defines family relations in this way...

- Parent = mother, father

- Child = daughter, son, stepdaughter, stepson

- Some children traveled only with a nanny, therefore parch=0 for them.

# Feature Engineering

The following Feature Engineering tasks were done.

- Expanded the acronym C, S, Q for the Embarked Variable with Cherbourg, Southampton & Queenstown respectively

- Expanded the acronym 1,2,3 for the Pclass Variable with !st Class, 2nd Class & 3rd Class respectively

- determined whether a passenger is a minor depending on his/her age(age <18) and stored that in a different variable.

- Created new variables age_group and age_range based on the passengers age.

- Determined whether a passenger is married or single from their name, age and sex.

- Determined Travel companion of the passengers out of Sibling/Spouse and Parent/Children data.

- Determined the fare_range from the fare variable.

- Filled the rows of Cabin Variable with 'Not in a Cabin" which were earlier empty. Else we would have to remove this variable as only 23% of the passengers had a cabin.
