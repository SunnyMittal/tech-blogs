---
title: "CLI commands"
date: 2024-06-30
---

# This is list of useful CLI commands

## [Dotnet](https://learn.microsoft.com/en-us/dotnet/core/tools/dotnet)

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
|          | dotnet sln add API.Demo          | Add project to the solution |
|          | dotnet sln API.Demo.sln list     | List projects in a sln file |
| | | |
| project | dotnet new webapi -minimal -f net8.0 \-\-output API.Demo                                                                                                            | Create new dotnet webapi project                                                        |
|         | dotnet new isef -lang c# \-\-output .\IdentityServer\                                                                                                               | Create new project for dotnet identity server with entity framework                     |
|         | dotnet new console -f net8.0 -n CustomerIterator                                                                                                                    | Create dotnet console application                                                       |
|         | dotnet list package \-\-outdated                                                                                                                                    | List outdated packages                                                                  |
|         | dotnet add package \<package names separated by space\>                                                                                                             | Update outdated packages                                                                |
|         | dotnet add .\SchemaCompare.Test.csproj reference  ..\SchemaCompare\SchemaCompare.csproj                                                                             | To add reference to SchemaCompare.csproj in the SchemaCompare.Test.csproj.              |
|         | dotnet remove reference ..\SchemaCompare\SchemaCompare.csproj                                                                                                       | Remove a project refernce.                                                              |
|         | <ItemGroup> <br> <Content Include=".\Abbreviations\abbreviations.csv"> <br> <CopyToOutputDirectory>Always</CopyToOutputDirectory> <br> </Content> <br> </ItemGroup> | To mark a file as copy always to output directory. Add these lines in the .csproj file. |
| | | |
| package | dotnet add package CommandLineParser | Install a nuget package using dotnet CLI |
| | | |
| file | dotnet new gitignore | Add gitignore file |
| run | dotnet run \-\-project .\Console.GetAzureBuildAgentIPs.csproj \-\- -f "C:\\Users\\USER\\Downloads\\ServiceTags_Public_20240805.json" -r "australiaeast" | Run console application passing arguments. Notice '\-\-' separating the arguments for the console application |
| | | |


## [Docker](https://docs.docker.com/reference/cli/docker/buildx/build/)

| Type | Command | Description |
| - | - | - |
| Image | docker images                                                                                      | Check docker images                                                   |
|       | docker create \-\-name api-typed-configuration-settings-container api-typed-configuration-settings | Create a container image                                              |
|       | docker build -t <image tag> -f Dockerfile .                                                        | Build container image for the app                                     |
|       | docker rmi demo:dev                                                                                | Remove a docer image                                                  |
|       | docker ps                                                                                          | List all running docker containers                                    |
|       | docker run \-\-rm -it -p 5180:5180/tcp apidemo:1.1.0                                               | Run docker image:tag interactively with port mapping, remove on close |
|       | docker run \-\-rm -d -p 5180:5180/tcp apidemo:1.1.0                                                | Run docker image:tag in detached mode with port mapping, remove later |
|       | docker stop 66f2b34a26f4                                                                           | Stop docker container with container id                               |
|       | docker logs <container-id>                                                                         | Monitor/Watch logs of a container                                     |
|       | docker top <container name>                                                                        | List UID, PID, PPID and other details                                 |
| | | |


## Kubernetes (K8s)
| Type | Command | Description |
| - | - | - |
| kubectl | kubectl apply -f deployment.yaml | Deploy a service to K8s cluster                                                        |
|         | kubectl get services             | Get K8s service external IP                                                            |
|         | kubectl port-forward service/myhelmapp 8888:80 --namespace dev | forward traffic from localhost:8888 to container port 80 |
| | | |
[Create powershell shortcut/alias for kubectl commands](https://manjit28.medium.com/powershell-define-shortcut-alias-for-common-kubernetes-commands-1c006d68cce2)
[Create bash shortcut/alias for kubectl commands](https://dev.to/zenika/kubernetes-a-pragmatic-kubectl-aliases-collection-17oc)

## Bash prompt for Linux
| Type | Command | Description |
| - | - | - |
| alias | alias k=kubectl | sets k as alias for kubectl command |

## Helm
| Type | Command | Description |
| - | - | - |
| | helm template . | Generate and display output files after applying variable values to yaml files in current working directory |
| | | |


## [Azure](https://learn.microsoft.com/en-us/cli/azure/reference-index?view=azure-cli-latest)

| Type | Command | Description |
| - | - | - |
| extensions | az extension list \-\-output table                                       | Check installed extensions                                                                 |
|            | az extension list \-\-query "[?name=='containerapp'].*" \-\-output table | Filter output of az cli command using [JMESPath](https://jmespath.org/tutorial.html) query |
| | | |
| acr | az acr login \-\-name <registry-name>                                                                                                   | login to an Azure container registry                 |
|     | az acr repository list \-\-name <registry-name> --output table                                                                          | List container images in an Azure container registry |
|     | az acr show-usage -n acr4aks20240809                                                                                                    | List size of all images in Azure container registry  |
|     | az acr repository show-manifests -n acr4aks20240809 \-\-repository dotnet8.api1 \-\-detail \-\-query '[].{Size: imageSize, Tags: tags}' | Get size for all tags of one repository              |
| | | |
| aks | az aks stop \-\-name aksCluster20240809 \-\-resource-group rg-aks-test  | Stop AKS cluster to save cost        |
|     | az aks show \-\-name aksCluster20240809 \-\-resource-group rg-aks-test  | Verify cluster is stopped or started |
|     | az aks start \-\-name aksCluster20240809 \-\-resource-group rg-aks-test | Start AKS cluster                    |
| | | |


## PowerShell

| Type | Command | Description |
| - | - | - |
| Battery | powercfg /batteryreport /output "C:\battery-report.html" | Exports the device battery report to html file |
| Version | $PSVersionTable | Check powershell version |
| | | |
| docker | Enable-WindowsOptionalFeature -Online -FeatureName VirtualMachinePlatform | Enable virtual machine platform on windows 11 for docker desktop installation |
| | | |
| file | New-Item .\Dockerfile | Create a file from powershell prompt. e.g. in VS code |
| | | |
| environment variable | $env:ACR_RGNAME='acr-01-RG'                                                                  | set an environment variable in active session |
|                      | $env:ACR_NAME=$(az acr list --resource-group $env:ACR_RGNAME --query "[].name" --output tsv) | use existing environment variable to get info |
| | | |
| alias | Set-Alias -Name k -Value kubectl | Sets 'k' as an alias for 'kubectl' |
| | | |


## Windows command line

| Type | Command | Description |
| - | - | - |
| Netstat | netstat -p tcp -ano \| findstr :10001 | Command to find which process is listening on a localhost port 10001 |
| | | |

## Java/Maven

| Type | Command | Description |
| - | - | - |
| | java -version | get java version installed on windows |
| | mvn -version | get maven version installed on windows |
| | mvn versions:display-dependency-updates | checks the dependency packages for which upgrade is available |
| | mvn versions:use-latest-releases | update all dependency packages to latest version |