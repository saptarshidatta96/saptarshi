---
published: true
layout: post
---
In the past two blog posts, I have shown how to wrap a ML Model inside a flask webservice and how to deploy the webservice on the Azure Platform.

Today, I will be demonstrating how am I going to access the web service, which can run either on our local host or deployed on a kubernetes cluster in Azure. Essentially, for this we need to create a client application and a User Interface to access the webservice. An free python library called [streamlit](https://streamlit.io/) provides just the same.

But before that, we need to understand, what are we trying to achieve here. We could have easily built a simple monolithic application that would have asked for user input and the model would have predicted an output based on that user input and deployed the same as an Azure Web Service. It may seem that wraping our model as a flask webservice was un-necessary. However, it is not!!

What if, we encounter a situation where the output of the ML model would be used by a downstream appliction thta is already running in Production. In that scenario, the client application might or moight not be coded in python where as python is the favourable language used by datascientists aound the world. To mitigate such issues, we need to have a mechanism for for python based models to interact with non-pythonic application. These type of applications are called microservcices. A microservice based architecture has several advantages and disadvantages, which is available [here](https://solace.com/blog/microservices-advantages-and-disadvantages/).

In this blog, I will be using streamlit to create an User Interface that will accept input from the users, and will call the flask web service to get the prediction. This application is out client application that will be accessing the flask webservice to get the desired output. Now, insted of being a User Interface, the client application could have been a part of an already existing system in Production.

The code for the user interface is available [here](https://github.com/saptarshidatta96/Breast-Cancer).

```
import requests
import json
import streamlit as st
import numpy as np
import pandas as pd
from werkzeug.wrappers import response 


url ='http://localhost:12345/predict'



st.title("Breast Cancer Prediction")

col1, col2,col3 = st.columns(3)

mean_radius = np.float(col1.text_input("mean radius",0))
mean_texture = np.float(col2.text_input("mean texture",0))
mean_perimeter = np.float(col3.text_input("mean perimeter",0))
mean_area = np.float(col1.text_input("mean area",0))
mean_smoothness = np.float(col2.text_input("mean smoothness",0))
mean_compactness = np.float(col3.text_input("mean compactness",0))
mean_concavity = np.float(col1.text_input("mean concavity",0))
mean_concave_points = np.float(col2.text_input("mean concave points",0))
mean_symmetry = np.float(col3.text_input("mean symmetry",0))
mean_fractal_dimension = np.float(col1.text_input("mean fractal dimension",0))
radius_error = np.float(col2.text_input("radius error",0))
texture_error = np.float(col3.text_input("texture error",0))
perimeter_error = np.float(col1.text_input("perimeter error",0))
area_error = np.float(col2.text_input("area error",0))
smoothness_error = np.float(col3.text_input("smoothness error",0))
compactness_error = np.float(col1.text_input("compactness error",0))
concavity_error = np.float(col2.text_input("concavity error",0))
concave_points_error = np.float(col3.text_input("concave points error",0))
symmetry_error = np.float(col1.text_input("symmetry error",0))
fractal_dimension_error = np.float(col2.text_input("fractal dimension error",0))
worst_radius = np.float(col3.text_input("worst radius",0))
worst_texture = np.float(col1.text_input("worst texture",0))
worst_perimeter = np.float(col2.text_input("worst perimeter",0))
worst_area = np.float(col3.text_input("worst area",0))
worst_smoothness = np.float(col1.text_input("worst smoothness",0))
worst_compactness = np.float(col2.text_input("worst compactness",0))
worst_concavity = np.float(col3.text_input("worst concavity",0))
worst_concave_points = np.float(col1.text_input("worst concave points",0))
worst_symmetry = np.float(col2.text_input("worst symmetry",0))
worst_fractal_dimension = np.float(col3.text_input("worst fractal dimension",0))


sample = [
    {
        "mean radius": mean_radius,
        "mean texture": mean_texture,
        "mean perimeter": mean_perimeter,
        "mean area": mean_area,
        "mean smoothness": mean_smoothness,
        "mean compactness": mean_compactness,
        "mean concavity": mean_concavity,
        "mean concave points": mean_concave_points,
        "mean symmetry": mean_symmetry,
        "mean fractal dimension": mean_fractal_dimension,
        "radius error": radius_error,
        "texture error": texture_error,
        "perimeter error": perimeter_error,
        "area error": area_error,
        "smoothness error": smoothness_error,
        "compactness error": compactness_error,
        "concavity error": concavity_error,
        "concave points error": concave_points_error,
        "symmetry error": symmetry_error,
        "fractal dimension error": fractal_dimension_error,
        "worst radius": worst_radius,
        "worst texture": worst_texture,
        "worst perimeter": worst_perimeter,
        "worst area": worst_area,
        "worst smoothness": worst_smoothness,
        "worst compactness": worst_compactness,
        "worst concavity": worst_concavity,
        "worst concave points": worst_concave_points,
        "worst symmetry": worst_symmetry,
        "worst fractal dimension": worst_fractal_dimension
    }
]

result = st.button("Predict")

if result:
    j_data = json.dumps(sample)
    headers = {'content-type': 'application/json', 'Accept-Charset': 'UTF-8'}
    response = requests.post(url, data=j_data, headers=headers)
    predictions =  json.loads(response.text)
    predictions = predictions["prediction"]
    
    if predictions[1] == 1:
        st.write('The patient has Breast Cancer')
    else:
        st.write('Breast Cancer has not been detected.')
```

The streamlit based User Interface that accepts user input looks like:
![]({{site.baseurl}}/images/streamlit-ui-microservice.PNG)

Now, we have come to the end of our 3 part blog series where we learnt to -

1. wrap a ML Application in a Flask Webservice and run it as a container in docker.

2. deploy the webservice on Azure Platform.

3. call the webservice from a client application.