---
published: true
---
In the past two blog posts, I have shown how to wrap a ML Model inside a flask webservice and how to deploy the webservice on the Azure Platform.

Today, I will be demonstrating how am I going to access the web service, which can run either on our local host or deployed on a kubernetes cluster in Azure. Essentially, for this we need to create a client application and a User Interface to access the webservice. An free python library called [streamlit](https://streamlit.io/) provides just the same.

But before that, we need to understand, what are we trying to achieve here. We could have easily built a simple monolithic application that would have asked for user input and the model would have predicted an output based on that user input and deployed the same as an Azure Web Service. It may seem that wraping our model as a flask webservice was un-necessary. However, it is not!!

What if, we encounter a situation where the output of the ML model would be used by a downstream appliction thta is already running in Production. In that scenario, the client application might or moight not be coded in python where as python is the favourable language used by datascientists aound the world. To mitigate such issues, we need to have a mechanism for for python based models to interact with non-pythonic application. These type of applications are called microservcices. A microservice based architecture has several advantages and disadvantages, which is available [here](https://solace.com/blog/microservices-advantages-and-disadvantages/).

In this blog, I will be using streamlit to create an User Interface that will accept input from the users, and will call the flask web service to get the prediction. This application is out client application that will be accessing the flask webservice to get the desired output. Now, insted of being a User Interface, the client application

