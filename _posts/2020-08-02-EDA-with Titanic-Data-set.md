---
layout: post
title: EDA with Titanic Data Set - Literature
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
