## Azure Key Vault Deployment with Bicep & GitHub Actions

Welcome to this tutorial on deploying an Azure Key Vault using Bicep and GitHub Actions! In this tutorial, we will walk through the steps necessary to set up a continuous deployment pipeline for an Azure Key Vault using these tools.

## Prerequisites

- An Azure subscription
- A GitHub account
- The Azure CLI installed on your local machine

## Setting up the Key Vault

1. First, create an Azure resource group to hold the Key Vault:

az group create --name myResourceGroup --location northeurope

2. Now, we need to set up a service principal and grant it permissions to access the Key Vault. First, create the service principal:

az ad sp create-for-rbac --name myServicePrincipal

This will output a JSON object containing the service principal's `clientId` and `clientSecret`. Save these for later use.

## Creating the Bicep file

1. Create a file named `KV.bicep` (https://github.com/Imadus00/AzureKeyVaultDeployment/blob/main/KV.bicep)
2. Create param.json to set variables (https://github.com/Imadus00/AzureKeyVaultDeployment/blob/main/param.json)

## Setting up GitHub Actions

1. Go to your repository on GitHub and navigate to the `Actions` tab.
2. Click the `Set up a workflow yourself` button.
3. Create a secret repository to login from the pipeline :
  - Go to settings then to secrets and click on actions
  - Click on create new secret repository
  - secret name = AZURE_CREDENTIALS
  - Value = paste the result you obtained when creating the service principal.  
  example : 
  {
  "clientId": "xxxxx-xxxxx-xxxxxxx",
  "clientSecret": "xxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "subscriptionId": "xxxxx-xxxxx-xxxxxxx",
  "tenantId": "xxxxx-xxxxx-xxxxxxx",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
![image](https://user-images.githubusercontent.com/122009354/210835862-4d238f7d-9a4a-4d07-825c-c8cd2b3677a0.png)

3. Use the following code to define the workflow:

https://github.com/Imadus00/AzureKeyVaultDeployment/blob/main/.github/workflows/blank.yml

