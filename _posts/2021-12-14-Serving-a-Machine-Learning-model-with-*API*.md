---
published: true
layout: post
---
Till now, all the blogs I've posted were basically leveraging CNN pre-tarined models to develop a model that was useful for our given use case. But from my experience at TCS Rapid Labs, I have learnt that training models is not enough. We not to serve them to make them usable across our production systems.

Now, once we have acknowledged this gap in our learning journey, there is one more thing we need to take account of. Most of the production grade systems and legacy application who are willing to leavrage the power of AI are essentially not written in Python. However, most of us are using Python to train our models. This is where we can use power of APIs.

In this blog, we will be learning to wrap our ML Models into an API. We will be building a simple classifier whose job is to classify a breast tumour as malignant or benign based on the features in the dataset. After that we will be saving the trained model(Serialization & Deserialization), exposing the functionality of the model as an API and testing the API using Postman. Additionally the entire setup is avialble as a Docker Image [here](https://hub.docker.com/repository/docker/saptarshidatta96/breast_cancer) and code is availble [here](https://github.com/saptarshidatta96/Breast-Cancer).

The model training script is uploaded at the GitHub Repository above and will not be discussed here. However, we will discuss about serializing the model as pickle file, deserializing it and exposing the functionality of the model as a Flask API. We will be using sk-learn's `joblib` library for this.





