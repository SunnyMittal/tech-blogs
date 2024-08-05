---
title: "Azure container app to Azure SQL DB"
date: 2024-08-05
---

This article describes how to connect a dotnet 8 web api hosted in Azure container app to Azure SQL DB using EF Core

## Create dotnet web API using VS Code
> dotnet new webapi -controllers -f net8.0 --output API.Container.Connect2AzureSQL

Add connection string to appsettings.development.json
```
"ConnectionStrings": {
    "AZURE_SQL_CONNECTIONSTRING": "Server=tcp:az-sql-db-20240803.database.windows.net,1433;Initial Catalog=az-sql-db;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;Authentication=Active Directory Default;"
  }
```

## Provision Azure container app
Provision an Azure container app with linux servers, configured with github repository, branch connection.
![Azure container app github repository configuration.](/tech-blogs/assets/images/azureContainerAppGithubConfiguration.png)

![Azure container app provisioning with github actions.](/tech-blogs/assets/images/createAzureContainerAppWithGithubActionsForImageDeployment.png)

## Publish API to Azure container app
Once code is pushed to github branch which is configured with Azure container app then the workflow action is automatically triggered and image build by github is pushed to azure container app.
Secrets are setup by the previous step, just needed to update the "appSourcePath" in the workflow to select the right subfolder.
![Setup auto build and deployment to container app via github action on specific repo branch and sub-folder within the repo.](/tech-blogs/assets/images/githubRepoWorkflowActionSetupDuringAzureContainerAppProvisioning.png)

## Test that web API hosted in Azure container app is accessible online
Verify via the API Url to make sure its deployed. Can also check by running get request in .http file.
e.g. https://api-2-connect-db.agreeablemushroom-e81d3416.australiaeast.azurecontainerapps.io/weatherforecast
![Verify via the API Url to make sure its deployed.](/tech-blogs/assets/images/verifyAzContainerAppIsLive.png)

## Enable managed identity on Azure container app
Goto the container app, select Identity from left side options, enable system assigned managed identity.

## Provision Azure SQL DB
Provision Azure SQL DB within the same resource group as Azure container app.

## Add Azure container app identity name to Azure SQL DB as a user with read and write permissions
**I enabled internet access to database for this step (Need to find better alternative to this).**
As needed to connect to db using Azure Data Studio and execute SQL scripts to add the Container app identity name to read and write roles in the database.
https://learn.microsoft.com/en-us/azure/app-service/tutorial-connect-msi-sql-database?tabs=vscode%2Cefcore%2Cdotnetcore

## Update dotnet web API to add person controller and connection to Azure SQL DB
Add person model, db context and controller with ability to post and get person.
Commit change and push to github to the same branch which was configured during Azure container app provisioning.
This will trigger the build and deploy of the app to Azure container app.

## Test that web API running on local is able to connect to Azure SQL DB in cloud
Use .http file to run post and get commands with appropriate body.

## Setup managed identity based connection between Azure container app and Azure SQL database
This can be done easily by setting up connection from Azure container app to Azure SQL database.
Which boils down to below commands.

```
az extension add --name containerapp
az extension add --name serviceconnector-passwordless --upgrade
az containerapp connection create sql --connection sql_faadc --source-id /subscriptions/ba5f0dd1-c406-4ac1-85e7-fe0ba5540610/resourceGroups/rg-web-api-db/providers/Microsoft.App/containerApps/api-2-connect-db --target-id /subscriptions/ba5f0dd1-c406-4ac1-85e7-fe0ba5540610/resourceGroups/rg-web-api-db/providers/Microsoft.Sql/servers/az-sql-db-20240803/databases/az-sql-db --client-type dotnet --system-identity -c api-2-connect-db-build523c8 --customized-keys AZURE_SQL_CONNECTIONSTRING=AZURE_SQL_CONNECTIONSTRING
```

## Test that web API running in cloud is able to call Azure SQL DB in cloud
Use .http file to send get, post requests to the Azure container app url hosted in cloud. 