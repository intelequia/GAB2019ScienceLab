# Global Azure Bootcamp 2019 - Science Lab
This project contains instructions to deploy the Global Azure Bootcamp 2019 Science Lab

# Quickstart
To quickly deploy the science lab using Azure Container Instances, click on the button below. 

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




