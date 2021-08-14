
POC Script 

ISSUE: Failed to resolve refrenece issue while pulling with ACR user name and pasword. Must supply, Servie priciple id and password to pull it in right way. 
============================================================================================================================================================

# Pull-ACR_image_in_AKS--403-Forbidden

# set this to the name of your Azure Container Registry.  It must be globally unique
MYACR=mikkyacr

# Run the following line to create an Azure Container Registry if you do not already have one
az acr create -n mikkyacr2 -g mikkyacrrg2 --sku basic

# Create an AKS cluster with ACR integration
az aks create -n mikkyAKSCluster -g mikkyaksrg --generate-ssh-keys --attach-acr $MYACR

az aks update -n mikkyAKSCluster -g mikkyaksrg --attach-acr mikkyacr

az acr import  -n mikkyacr2 --source docker.io/library/nginx:latest --image nginx:v1

az aks get-credentials -g mikkyaksrg -n mikkyAKSCluster

Service principal ID: 1a179f4a-8sdsdsdaaaaa-54de30
Service principal password: 5Dyz2dF_5---dsds6YAXFU.

kubectl create secret docker-registry mikkysecret --docker-server=mikkyacr2.azurecr.io --docker-username=1a179sdsdsds-4fcd-026554de30 --docker-password=5Dyz2dF_>>>jKP2olx6YAXFU.

apiVersion: v1
kind: Pod
metadata:
  name: my-awesome-app-pod1
spec:
  containers:
    - name: main-app-container
      image: mikkyacr2.azurecr.io/nginx:v1
      imagePullPolicy: IfNotPresent
  imagePullSecrets:
    - name: mikkysecret
    
    
