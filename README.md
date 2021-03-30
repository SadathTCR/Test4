# ASP.NET Core
# Build and test ASP.NET Core projects targeting .NET Core.
# Add steps that run tests, create a NuGet package, deploy, and more:
# https://docs.microsoft.com/azure/devops/pipelines/languages/dotnet-core
 
trigger:
- main
 
pool:
  vmImage: 'ubuntu-latest'
 
variables:
  buildConfiguration: 'Release'
 
 
steps:
- script: dotnet build Sample/Sample/Sample.csproj --configuration $(buildConfiguration)
  displayName: 'dotnet build Sample/Sample/Sample.csproj $(buildConfiguration)'
 
- task: DotNetCoreCLI@2
  inputs:
    command: 'publish'
    publishWebProjects: false
    projects: '**/Sample.csproj '
    arguments: '--configuration $(buildConfiguration) --output $(Build.ArtifactStagingDirectory) /p:EnvironmentName=Production'
 
- task: PublishBuildArtifacts@1
  inputs:
      targetPath: '$(Build.ArtifactStagingDirectory)'

```
