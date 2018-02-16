# TeamCity base project configurations by tecnologies

## Tech availables
- [x] ASP.NET
- [ ] Nodejs
- [ ] PHP
- [ ] Golang


TODO: 
- Add other enviroments,  golang next maybe ?

### Setup ASP.NET CI/CD

This approach use the [web deploy] (https://www.iis.net/downloads/microsoft/web-deploy) package which allow us to make the procces faster, sadly includes a little bit more of configuraion and knowledge about what you are doing, trust me a suffer a lot to do this.

1. Create a parent project, name how you want
2. Create general build configuration
    - This project will have the connection to VCS (githug, gitlab...)
    - Create Build Steps 
        - Install NuGet packages
        - Build with MSBuild. You have to point to the correct file (depends on the project), commonly the solution file (.sln) but it can be a .csproj or .publishproj file. Command line parameters: `/p:DeployOnBuild=true;Configuration=Release;PublishProfile=Dev`

        Steps ![alt text](https://raw.githubusercontent.com/nosnibor89/tc-templates/master/img/aspnet-steps.PNG)

        MSBuild Step ![alt text](https://raw.githubusercontent.com/nosnibor89/tc-templates/master/img/aspnet-msbuild.PNG)
    - Set artifacts paths for your web deploy package

      MSBuild Step ![alt text](https://raw.githubusercontent.com/nosnibor89/tc-templates/master/img/aspnet-artifacts.PNG)


3. Create deployment configuration
    - Add Dependencies. Take snapshot for previous build config (Step 2) and add artifact dependency for the artifcacts in last step (same chain) 

    Artifacts deps: ![alt text](https://raw.githubusercontent.com/nosnibor89/tc-templates/master/img/aspnet-snapshot.PNG)
    - Add build step for webdeploy. This can be a command line step. 

    Artifacts deps: ![alt text](https://raw.githubusercontent.com/nosnibor89/tc-templates/master/img/aspnet-webdeploy.PNG)
    
