---
title: "Azure Functions"
date: 2024-07-01
---

# Azure functions

- Need to have Azure function core tools installed using x64 msi on windows 11 machine
https://github.com/Azure/azure-functions-core-tools?tab=readme-ov-file

- Install Azure CLI latest version

- Uninstall older version of azure function core tools as that might interfere with creation of azure function using cli

__*Note: if you need to see detailed logs then append ```--debug``` at the end of any az command.*__

## Install Azurite for running function locally

### Option 1
- Install "Azurite" extention in VS Code
- ctrl + shift + p and then choose "Azurite: start" command

### Option 2
- Install azurite using npm

    ```npm install -g azurite```

- Start Azurite using below command

    ```azurite -s -l c:\tools\azurite -d c:\tools\azurite\debug.log```

## Create Azure function project and function in VS Code
- ctrl + shift + p
- choose "Azure Functions: Create New Project.."
- answer questions that follow
- Add function to existing Azure Function project
    - ctrl + shift + p
    - choose "Azure Functions: Create Function.."
    - answer questions that follow

## Publish Function to Azure using Azure CLI
- if needed cd into the azure function folder in VS Code terminal. e.g. C:\D\W\Samples\Func.ServiceBusMessageProcessor
- set environment variable ```$RESOURCE_GROUP="rg-service-bus"```
- set environment variable ```$LOCATION="australiaeast"```
- set environment variable ```$RUNTIME="dotnet-isolated"```
- set environment variable ```$FUNCTIONS_VERSION=4```
- set environment variable ```$FUNCTION_NAME="func-sb-message-processor"```
- set environment variable ```$STORAGE_ACCOUNT_NAME="storage20240722"```
- set environment variable ```$WEBSITE_CONTENTSHARE="func-sb-message-processor20240722"```

- create function storage account separately
    > az storage account create
        --name $STORAGE_ACCOUNT_NAME
        --resource-group $RESOURCE_GROUP
        --location $LOCATION
        --sku Standard_RAGRS
        --kind StorageV2
        --min-tls-version TLS1_2
        --allow-blob-public-access false

- create function app in Azure
    > az functionapp create
        --resource-group $RESOURCE_GROUP
        --consumption-plan-location $LOCATION
        --runtime $RUNTIME
        --functions-version $FUNCTIONS_VERSION
        --name $fUNCTION_NAME
        --storage-account $STORAGE_ACCOUNT_NAME

## Enable managed identity for function app
![Enable function app managed identity via azure portal](/tech-blogs/assets/images/enableFuncAppManagedIdentityViaAzurePortal.png)

## Allow read permission for azure function managed identity on service bus queue
![Add permission for function app managed identity on service bus via azure portal](/tech-blogs/assets/images/addFuncManagedIdentityPermissionOnSB.png)

## Publish function to Azure (this step didn't work properly)
    - ctrl + shift + p
    - choose "Azure Functions: Deploy to Function App"
    - select the function app created in step above the publish step

