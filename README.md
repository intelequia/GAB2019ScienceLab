![Global Azure Bootcamp 2019 - Science Lab](https://github.com/intelequia/GAB2019ScienceLab/raw/master/images/ScienceLab2019.jpg)

# Global Azure Bootcamp 2019 - Science Lab
This project contains instructions to deploy the Global Azure Bootcamp 2019 Science Lab

# Quickstart
To quickly deploy the science lab using Azure Container Instances, click on the button below. **If it's your first deployment, we strongly recommend to read the instructions below.**

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FIntelequia%2FGAB2019ScienceLab%2Fmaster%2Flab%2FGABClient.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

# Introduction
This project contains all the source code for the Global Azure Bootcamp 2019 Science Lab. Created by David Rodriguez ([@davidjrh](http://twitter.com/davidjrh)), Martin Abbott ([@martinabbott](http://twitter.com/martinabbott)) and Santiago Porras ([@saintwukong](http://twitter.com/saintwukong)) for the Global Azure Bootcamp 2019 Science Lab running Enric Pallé, Diego Hidalgo and Sebastian Hidalgo's Machine Learning algorithms for exoplanet hunting at the [Instituto de Astrofisica de Canarias](http://www.iac.es/index.php?lang=en) using TESS mission data from NASA.

See more at https://global.azurebootcamp.net/global-azure-science-lab-2019/

# Getting Started

## Requirements

In order to participate on the GAB Science Lab you will need:
* An active Azure subscription. The easiest way to deploy the lab is by using Azure Container Instances. You will need an active Azure subscription to deploy the containers on Azure. You can signup for a free subscription [here](https://azure.microsoft.com/free/) or use the Azure Passes shared on the Global Azure Bootcamp event. 
* You can deploy the client on any other Docker powered environment:
    * locally on your laptop using Docker Desktop, follow instructions at https://www.docker.com/products/docker-desktop
    * on any other environment, check https://docs.docker.com/install/

## Deploying the lab using Azure Container Instances (ACI)
The easiest way to deploy the Science Lab is by using Azure Container Instances. We have prepared a resource manager template that simplifies this step, by asking you some parameters that are used in the container that will be used later on the Global Dashboards for statistics and for fun. 
1. Click on the deployment button below to start the process:

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FIntelequia%2FGAB2019ScienceLab%2Fmaster%2Flab%2FGABClient.json" target="_blank">
    <img src="http://azuredeploy.net/deploybutton.png"/>
</a>

2. Fill the form. You can get info about each field if you hold the cursor over the info icon.
    * Choose the subscription and resource group you where you want to deploy the container instances
    * **Location**: **IMPORTANT: the Azure Container Instances service is not available in all the regions**. At time of writing, you must choose between one of these locations:
        * "Central US"
        * "East US"
        * "East US2"
        * "North Central US"
        * "South Central US"
        * "West US"
        * "West US2"
        * "North Europe"
        * "West Europe"
        * "East Asia"
        * "Southeast Asia"
        * "Japan East"
        * "Australia East"
        * "Central India"
        * "South India"
        * "Canada Central"
    * **Email, FullName, TeamName, CompanyName**: fill with your personal info. It be displayed on the global dashboards (e-mail will not)
    * **CountryCode**: the 2 character ISO2 country code. Find your code at [Wikipedia](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2)
    * **LabKeyCode**: Is a predefined string with your location LAB Key. Ask admin staff at your location for the code. If you don't know any, just use THE-GAB-ORG as key.    
    * **InstanceCount**: Number of container instance groups (60 or less, there is a limit of 60 ACIs per Azure susbcription). Check the available instances/quotas in your subscription before setting up a big number. TIP: You can start with 1 or 2 container instance groups and repeat this process later to deploy more instances

Click on the Accept the Terms and Conditions checkbox, and relax waiting for the green check. Will take around 5 minutes to complete.

# Verifying the lab is working properly
Once the lab has been deployed, you will see a set of resources under the resource group, one per container instance group. Each group will container just one container instance. 

Click on one of the container instances, and get the public DNS name from the General Settings area. Browse the URL and you would be able to see if the lab is working properly. There are three areas:
* **Inputs Downloaded**: a green light indicates that is working properly. Every 10 seconds a background process checks if there are no inputs to process, and then downloads a new batch of inputs;
* **Processing**: a green light indicates that is working properly. A background process starts processing the inputs as soon as they are available locally. The inputs are processed one by one and results are saved into an internal output queue;
* **Ouputs Uploaded**: a green light indicates that is working properly. Every 10 seconds a background process checks if there are outputs ready to be uploaded to the GAB server.

There is also a log area where you can check what is happening inside the GAB client.

# Decomissioning the Science Lab
Your lab deployment will continue working processing inputs until you delete the deployment resources. Note that this year our intention is to continue processing information after the GAB day. 

In order to delete your deployment:
1. Select the Resource Group containing your science lab deployment
2. Click on Delete and confirm by typing your resource group name

Thanks for your support on Global Azure Bootcamp 2019 Science Lab. Live Long and Prosper!

# Frequently Asked Questions
1. **How much will cost?**

The lab uses an Azure Container Instances. The cost of each ACI would be around $1 for a full day (consumption 1vCPU and 1GB RAM over 24h).  
So for example, if you deploy the science lab with 4 container instances during 12 hours, the costs would be under $2.
For more information about pricing:
* [Azure Container Instances](https://azure.microsoft.com/en-us/pricing/details/container-instances/)

