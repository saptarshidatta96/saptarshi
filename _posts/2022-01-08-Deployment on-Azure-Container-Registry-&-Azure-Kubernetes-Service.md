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
Once we have completed completed the above steps, we should check whether the resources have been created properly in the Azure Portal. Next, we will login to the Container registry, tag the local docker image to that of the container Registry, and then push it to the container registry.

```
#Login to ACR
az acr login -n breastcancersd

#Tag a Docker Image to ACR
docker tag breast_cancer:latest breastcancersd.azurecr.io/breast_cancer:v1.0

#Push the image to ACR
docker push breastcancersd.azurecr.io/breast_cancer:v1.0
```

Once done, we should verify that the image is present in the Container Registry. Next, we

```
#Enable Admin Credentials on the ACR
az acr update -n breastcancersd --admin-enabled true

#Run the Azure Container Instance
az container create --resource-group trial-rg --name breast-cancer --image breastcancersd.azurecr.io/breast_cancer:latest --cpu 1 --memory 1 --registry-login-server breastcancersd.azurecr.io --registry-username breastcancersd --registry-password sNmi=CIMYKkzt86WLvuFEm7HrOPeMlpc --dns-name-label breastcancerapp --ports 12345

az container show --resource-group trial-rg --name breast-cancer --query instanceView.state

az container show --resource-group trial-rg --name breast-cancer --query ipAddress.fqdn

#View Logs
az container logs --resource-group trial-rg --name breast-cancer
```
Once the conatiner instance is running, we can run the below access the service by

![]({{site.baseurl}}/images/ACR.PNG)

Run the below command to delete the resource group to prevent Recurring Charges.

```
az group delete --name trial-rg
```
