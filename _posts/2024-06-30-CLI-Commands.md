---
title: "CLI commands"
date: 2024-06-30
---

# This is list of useful CLI commands

## dotnet

| Type          | Command     | Description |
| ------------- | ----------- | ----------- |
| winget | winget list --name azure function                         | List packages filtered by name   |
|        | winget install -e --id Microsoft.Azure.FunctionsCoreTools | Install package                  |
|        | winget install -e --id Microsoft.AzureCLI                 | Install Azure CLI latest version |
| | | |
| choco | choco uninstall azure-functions-core-tools-3 | Uninstall package using choco |
| | | |
| Runtime | dotnet --list-runtimes | List .net runtimes |
| | | |
| dotnet Templates | dotnet new list | List all dotnet cli templates |
| | | |
| Solution | dotnet new sln --name API.Demo | Create a new solution file  |
|          | dotnet sln add API.Demo        | Add project to the solution |
|          | dotnet sln API.Demo.sln list   | List projects in a sln file |
| | | |
| Project | dotnet new webapi -minimal -f net8.0 --output API.Demo | Create new dotnet webapi project                                    |
|         | dotnet new isef -lang c# --output .\IdentityServer\    | Create new project for dotnet identity server with entity framework |
|         | dotnet new console -f net8.0 -n CustomerIterator       | Create dotnet console application                                   |
| | | |
| File | dotnet new gitignore | Add gitignore file |


## Docker

| Type | Command | Description |
| - | - | - |
| Image | docker images                                                                                    | Check docker images               |
|       | docker create --name api-typed-configuration-settings-container api-typed-configuration-settings | Create a container image          |
|       | docker build -t <image tag> -f Dockerfile .                                                      | Build container image for the app |
| | | |

## Windows command line
| Type | Command | Description |
| - | - | - |
| Netstat | netstat -p tcp -ano \| findstr :10001 | Command to find which process is listening on a localhost port 10001 |
| | | |