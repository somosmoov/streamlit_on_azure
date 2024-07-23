# Deploying Streamlit Application on Azure App Service
To deploy a Streamlit application on Azure App Service, follow these steps:

Create an Azure App Service with B1 SKU or higher, as the free version does not support Streamlit.

Choose Python v3.10 or above for Streamlit in the App Service.

Choose Linux as the operating system for the App Service.

Make sure your code folder has a requirements.txt file with all the dependencies.

Create a bash script run.sh, and write the following command in it

Deploying Streamlit Application on Azure App Service

## Firstly get an azure subscription if you don't have one, create a free trial, then install azure CLI in your system.

Login to ur azure ACC.

Bash

Copy
az login

Create a new resource group (replace ResourceGroupName and Region with your preferred values).

Bash

Copy
az group create --name ResourceGroupName --location Region

Create a serviceplan

Bash

Copy
az appservice plan create --name PlanName --resource-group ResourceGroupName --sku B1 --is-linux

Now create a webapp

Bash

Copy
az webapp create --name AppName --resource-group ResourceGroupName --plan PlanName --runtime "python|3.8"

Streamlit's default configuration is for development. Modify your Streamlit app to include the following lines at the end:

Python

Copy
app.py  import streamlit as st  # Your Streamlit app code here  if __name__ == '__main__':     st.set_option('server.enableCORS', True) 
Deploy your Streamlit app to Azure using Git. Initialize a Git repository in your Streamlit project if you haven't already.

Bash

Copy
git init

git remote add azure <git-url-from-azure>

Now finally push your code to azure.

Bash

Copy
git add .
git commit -m "Initial commit"
git push azure master

That's it! Your Streamlit app should now be deployed.
