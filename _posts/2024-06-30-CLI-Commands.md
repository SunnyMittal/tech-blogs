---
title: "CLI commands"
date: 2024-06-30
---

# This is list of useful CLI commands

## dotnet

| Type          | Command     | Description |
| ------------- | ----------- | ----------- |
| winget | winget list --name azure function                         | List packages filtered by name   |
|        | winget install -e \-\-id Microsoft.Azure.FunctionsCoreTools | Install package                  |
|        | winget install -e \-\-id Microsoft.AzureCLI                 | Install Azure CLI latest version |
| | | |
| choco | choco uninstall azure-functions-core-tools-3 | Uninstall package using choco |
| | | |
| runtime | dotnet \-\-list-runtimes | List .net runtimes |
| | | |
| dotnet Templates | dotnet new list | List all dotnet cli templates |
| | | |
| solution | dotnet new sln \-\-name API.Demo | Create a new solution file  |
|          | dotnet sln add API.Demo        | Add project to the solution |
|          | dotnet sln API.Demo.sln list   | List projects in a sln file |
| | | |
| project | dotnet new webapi -minimal -f net8.0 \-\-output API.Demo | Create new dotnet webapi project                                    |
|         | dotnet new isef -lang c# \-\-output .\IdentityServer\    | Create new project for dotnet identity server with entity framework |
|         | dotnet new console -f net8.0 -n CustomerIterator       | Create dotnet console application                                   |
|         | dotnet list package \-\-outdated                         | List outdated packages                                              |
|         | dotnet add package <package names separated by space>  | Update outdated packages                                            |
| | | |
| package | dotnet add package CommandLineParser | Install a nuget package using dotnet CLI |
| | | |
| file | dotnet new gitignore | Add gitignore file |
| run | dotnet run \-\-project .\Console.GetAzureBuildAgentIPs.csproj \-\- -f "C:\\Users\\USER\\Downloads\\ServiceTags_Public_20240805.json" -r "australiaeast" | Run console application passing arguments. Notice '\-\-' separating the arguments for the console application |
| | | |


## Docker

| Type | Command | Description |
| - | - | - |
| Image | docker images                                                                                    | Check docker images                    |
|       | docker create \-\-name api-typed-configuration-settings-container api-typed-configuration-settings | Create a container image               |
|       | docker build -t <image tag> -f Dockerfile .                                                      | Build container image for the app      |
|       | docker logs <container-id>                                                                       | Monitor/Watch logs of a container      |
|       | docker top <container name>                                                                      | List UID, PID, PPID and other details  |
| | | |


## [Azure](https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)

| Type | Command | Description |
| - | - | - |
| extensions | az extension list \-\-output table                                     | Check installed extensions                                                                 |
|            | az extension list \-\-query "[?name=='containerapp'].*" \-\-output table | Filter output of az cli command using [JMESPath](https://jmespath.org/tutorial.html) query |
| | | |
| acr | az acr login \-\-name <registry-name>                                                                                               | login to an Azure container registry                 |
|     | az acr repository list \-\-name <registry-name> \-\-output table                                                                      | List container images in an Azure container registry |
|     | az acr show-usage -n acr4aks20240809                                                                                              | List size of all images in Azure container registry  |
|     | az acr repository show-manifests -n acr4aks20240809 \-\-repository dotnet8.api1 \-\-detail \-\-query '[].{Size: imageSize, Tags: tags}' | Get size for all tags of one repository |
| | | |
| aks | az aks stop \-\-name aksCluster20240809 \-\-resource-group rg-aks-test  | Stop AKS cluster to save cost        |
|     | az aks show \-\-name aksCluster20240809 \-\-resource-group rg-aks-test  | Verify cluster is stopped or started |
|     | az aks start \-\-name aksCluster20240809 \-\-resource-group rg-aks-test | Start AKS cluster                    |
| | | |


## PowerShell

| Type | Command | Description |
| - | - | - |
| Battery | powercfg /batteryreport /output "C:\battery-report.html" | Exports the device battery report to html file |


## Windows command line

| Type | Command | Description |
| - | - | - |
| Netstat | netstat -p tcp -ano \| findstr :10001 | Command to find which process is listening on a localhost port 10001 |
| | | |