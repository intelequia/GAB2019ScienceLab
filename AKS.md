![Global Azure Bootcamp 2019 - Science Lab](https://github.com/intelequia/GAB2019ScienceLab/raw/master/images/ScienceLab2019.jpg)

# Global Azure Bootcamp 2019 - Science Lab
This project contains instructions to deploy the Global Azure Bootcamp 2019 Science Lab

# Quickstart
To quickly deploy the science lab using Azure Container Instances, click on the button below. **If it's your first deployment, we strongly recommend to read the instructions below.**

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Ffaug%2FGlobalAzure%2Fmaster%2FScienceLab%2Flab%2FGABClient.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

https://github.com/faug/GlobalAzure/

# Introduction
This project contains all the source code for the Global Azure Bootcamp 2019 Science Lab. Created by David Rodriguez ([@davidjrh](http://twitter.com/davidjrh)), Martin Abbott ([@martinabbott](http://twitter.com/martinabbott)) and Santiago Porras ([@saintwukong](http://twitter.com/saintwukong)) for the Global Azure Bootcamp 2019 Science Lab running Enric Pallé, Diego Hidalgo and Sebastian Hidalgo's Machine Learning algorithms for exoplanet hunting at the [Instituto de Astrofisica de Canarias](http://www.iac.es/index.php?lang=en) using TESS mission data from NASA.

See more at https://global.azurebootcamp.net/global-azure-science-lab-2019/

# Getting Started

## Requirements

In order to participate on the GAB Science Lab you will need:
* An active Azure subscription. The easiest way to deploy the lab is by using Azure Container Instances. You will need an active Azure subscription to deploy the containers on Azure. You can signup for a free subscription [here](https://azure.microsoft.com/free/) or use the Azure Passes shared on the Global Azure Bootcamp event. 
* You can deploy the client on any other Docker powered environment (see deployment instructions at the end of this document):
    * locally on your laptop using Docker Desktop, follow instructions at https://www.docker.com/products/docker-desktop
    * on any other environment, check https://docs.docker.com/install/

## Deploying the lab using Azure Kubernetes Service (AKS)
1. First, you need to create an Azure Kuberetes Service cluster. You can do it from AZ CLI or from Cloud Shell (https://shell.azure.com):

``` shell
az login
az group create -n "resource-group-name" -l WestEurope
az aks create -g "resource-group-name" -n "aks-unique-cluster-name" --generate-ssh-keys

```

Please see https://docs.microsoft.com/en-us/azure/aks/kubernetes-walkthrough for more details.

2. Once you have deployed you AKS cluster, connect to it and deploy the Service Manifest by running the following command:

``` shell
az aks get-credentials -g "resource-group-name" -n "aks-unique-cluster-name"
wget https://raw.githubusercontent.com/faug/GlobalAzure/master/ScienceLab/kubernetes/globalscience-hki.yml
nano globalscience-hki.yml
kubectl apply -f ./globalscience-hki.yml
```


# Verifying the lab is working properly (AKS)
Wait until the external IP address of the service is provisioned by running the following:

``` shell
kubectl get services -w
```


![AKS URL](https://raw.githubusercontent.com/faug/GlobalAzure/master/ScienceLab/kubernetes/Deployment8.png)

Copy the EXTERNAL IP address and navigate to it using browser. You will be able to see if the lab is working properly. There are three areas:
* **Inputs Downloaded**: a green light indicates that is working properly. Every 10 seconds a background process checks if there are no inputs to process, and then downloads a new batch of inputs;
* **Processing**: a green light indicates that is working properly. A background process starts processing the inputs as soon as they are available locally. The inputs are processed one by one and results are saved into an internal output queue;
* **Ouputs Uploaded**: a green light indicates that is working properly. Every 10 seconds a background process checks if there are outputs ready to be uploaded to the GAB server.

There is also a log area where you can check what is happening inside the GAB client.

![AKS Deployment completed](https://raw.githubusercontent.com/faug/GlobalAzure/master/ScienceLab/kubernetes/Deployment7.png)

Each input takes around 5 minutes to be processed by a container (pipeline 1 + pipeline 2 execution times). After the input is processed, it goes to the upload queue, and once uploaded, you start appearing on the Global Azure Bootcamp Science lab Dashboards, available at https://gablabdashboard.azurewebsites.net. 

# Decomissioning the Science Lab
Your lab deployment will continue working processing inputs until you delete the deployment resources. Note that this year our intention is to continue processing information after the GAB day. 

In order to delete your deployment:
1. Select the Resource Group containing your science lab deployment
2. Click on Delete and confirm by typing your resource group name

Thanks for your support on Global Azure Bootcamp 2019 Science Lab. Live Long and Prosper!

# Frequently Asked Questions
1. **How much will cost?**

The lab uses an Azure Kubernetes Service. You will only pay for computing which is 40$ for each node. Default deployment is 3 which is around 120$
For more information about pricing:
* [Azure Kubernetes Service](https://azure.microsoft.com/en-us/pricing/details/kubernetes-service/)

2. **How many instances can I deploy?**

If you are deploying the lab using Azure Kubernetes Service, there is a limit of vcores per Azure Subscription. You can deploy more than 10 if you use more subscriptions, but please, do the math following FAQ #1. Remember you can also deploy the science lab on your own laptop or on any other Docker powered environment.

3. **Can I start crunching data before April 27th?**

You can deploy the lab before April 27th just for testing purposes, but note that we will reset all the data, stats and dashboards on April 27th. 

4. **Can I continue processing data after April 27th?**

Yes, this year we want to continue hosting the Science Lab after the Global Azure Bootcamp day. Our intention is to continue processing data until the end of the TESS mission.

# Running the lab outside Azure
You can also run the science lab client on Windows, Linux or Mac, just because is implemented as a Docker container. The container image is available at Docker Hub https://hub.docker.com/r/globalazurebootcamp/sciencelab2019

You can deploy the client on any other Docker powered environment:
* locally on your Windows/Mac laptop using Docker Desktop, follow instructions at https://www.docker.com/products/docker-desktop
* on any other environment, check https://docs.docker.com/install/

## Deploying a local container with the science lab client
Once you have Docker installed locally, follow this steps:

1. Create a text file called `variables.env` with the following data (replace the values with your own data):
```
BatchClient__Email=johndoe@foo.com
BatchClient__Fullname=John Doe
BatchClient__TeamName=Global Azure Team
BatchClient__CompanyName=Global Azure Bootcamp Org.
BatchClient__CountryCode=XX
BatchClient__LabKeyCode=THE-GAB-ORG
```

2. Run the following Docker command:
```
docker run -d -p 8080:80 --env-file variables.env --restart always globalazurebootcamp/sciencelab2019:latest
```

This downloads the science lab client image and runs it on a container instance. If you browse http://localhost:8080, you will notice how the science lab is progressing.

## Deleting the science lab client on a local environment
Once you want to stop running the science lab, run the following commands:
1. Search the container id by executing the following command and writing down the container id with the name "globalazurebootcamp/sciencelab2019:latest"
```
docker ps -l
```

2. Run the command to delete the container instance:
```
docker rm <containerid> -f
```

# Troubleshooting

## I'm seeing "Minimum client version must be GAB.Client/1.x.x.x. Please, upgrade your container instance to the latest version" on the logs
This is because we needed to break the backwards compatibility with the previous client, and you need to redeploy your container. When running on Azure Container instances, this can be easily accomplished by clicking on the "Restart" button available on the Overview section of your container when using the Azure Portal. 
