---
published: true
layout: post
publisher: true
---
In the previous [post](https://saptarshidatta.in/2021/12/14/serving-machine-learning-model-with-api.html), we wrapped out ML Model inside a Flask Web Service which we could access through GET and POST Requests. Once, we found the application running perfectly on out local system, we  containerised the application and pushed it to [docker hub](https://hub.docker.com/r/saptarshidatta96/breast_cancer).


Today, we're going to take it up a notch further and will deploy the service on Azure Cloud Service.
At first, we will create a resource group and will then create an Azure Container Registry within that resource group. Every Azure Service that we are going to create will be inside our Resource Group. We have names our resource group as `trial-rg`. The name of the Azure Container Registry is `breastcancersd`.


We will be using Azure CLI for running the commands.

```
#Create A Resource Group
az group create --name trial-rg --location centralindia

#Get Subscription
az account show --output table

#Create ACR
az acr create  --resource-group trial-rg  --name breastcancersd --sku Basic
```
Once we have completed completed the above steps, we should check whether the resources have been created properly in the Azure Portal. Next, we

