---
published: true
layout: post
---
Till now, all the blogs I've posted were basically leveraging CNN pre-tarined models to develop a model that was useful for our given use case. But from my experience at TCS Rapid Labs, I have learnt that training models is not enough. We not to serve them to make them usable across our production systems.

Now, once we have acknowledged this gap in our learning journey, there is one more thing we need to take account of. Most of the production grade systems and legacy application who are willing to leavrage the power of AI are essentially not written in Python. However, most of us are using Python to train our models. This is where we can use power of APIs.

In this blog, we will be learning to wrap our ML Models into an API. We will be building a simple classifier whose job is to classify a breast tumour as malignant or benign based on the features in the dataset. After that we will be saving the trained model(Serialization & Deserialization), exposing the functionality of the model as an API and testing the API using Postman. Additionally the entire setup is avialble as a Docker Image [here](https://hub.docker.com/repository/docker/saptarshidatta96/breast_cancer) and code is availble [here](https://github.com/saptarshidatta96/Breast-Cancer).

The model training script is uploaded at the GitHub Repository above and will not be discussed here. However, we will discuss about serializing the model as pickle file, deserializing it and exposing the functionality of the model as a Flask API. We will be using sk-learn's `joblib` library for this.

```python
import joblib
joblib.dump(model, 'breast_cancer_knn_model.pkl')
model_columns = list(cancer_data['feature_names'])
joblib.dump(model_columns, 'model_columns.pkl')
```
Here, the object `model` refers to our trained model and the `model_columns` contains the list of columns in the dataset. We will serialize both of these as .pkl file. The reason for serializing `model_columns` is explained below.

```
from flask import Flask, request, jsonify
import joblib
import pandas as pd

app = Flask(__name__)

@app.route('/predict', methods=['POST'])
def predict():
    if knn_model:
        try:
            json_ = request.json
            print(json_)
            query = pd.get_dummies(pd.DataFrame(json_))
            query = query.reindex(columns=model_columns, fill_value=0)
            prediction = list(knn_model.predict(query))
            return jsonify({'prediction': str(prediction)})
        except Exception as e:
            return jsonify({'error': e})
    else:
        print ('Train the model first')
        return ('No model here to use')

if __name__ == '__main__':

    knn_model = joblib.load("breast_cancer_knn_model.pkl")
    print ('Model loaded')
    model_columns = joblib.load("model_columns.pkl")
    print ('Model columns loaded')
    app.run(host='0.0.0.0', port=12345, debug=True)
```







