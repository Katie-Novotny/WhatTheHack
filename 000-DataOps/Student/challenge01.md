# What the Hack: DevOps 

## Challenge 1 - Basic DevOps with SQL Database Project
[Back](challenge00.md) - [Home](../readme.md) - [Next](challenge02.md)

### Introduction

We can only assume that you are doing this What the Hack because you understand the importance of DataOps, however please take a moment to review these brief articles about the basic motivation behind DataOps.

1. [What is DataOps?](https://docs.microsoft.com/en-us/azure/devops/learn/what-is-devops)
2. [What features and services do I get with Azure DevOps?](https://docs.microsoft.com/en-us/azure/devops/user-guide/services)


### Challenge

### Install SQL Server Data Tools

1. Start Visual Studio Installer.
1. Select the "Data storage and processing" toolset. Make sure at least "SQL Server Data Tools is selected" under Installation details.
![Select SQL Server Data Tools](images/01-install-sql-server-data-tools.jpg)
1. Click Install.

### Create a SQL Server Database Project in Azure DevOps

1. Access Azure DevOps from a browser on the machine where you installed Visual Studio.

1. Create a new project in Azure DevOps for the sample database.
![Create a new DevOps project](images/02-create-devops-project.jpg)

1. Initialize the project's repository with the Visual Studio `.gitignore`.
![Initialize the project's repository with the Visual Studio .gitignore](images/03-initialize-repository.jpg)

1. Clone the repository in Visual Studio.
![Clone the repository in Visual Studio](images/04-clone-repository-01.jpg)
![Clone the repository in Visual Studio](images/04-clone-repository-02.jpg)

1. Proceed with the following steps in Visual Studio (it should open automatically, if not already running).
![Clone the repository in Visual Studio](images/04-clone-repository-03.jpg)

1. Create a new solution.<br/>
![Create a new solution](images/05-create-solution.jpg)

1. Create a SQL Server Database Project (leave the project name to "Database1").
![Create a SQL Server Database Project](images/06-create-database-project-01.jpg)
![Create a SQL Server Database Project](images/06-create-database-project-02.jpg)

1. Configure the project to target Azure SQL Database.
![Configure the project to target Azure SQL Database](images/07-configure-database-project-01.jpg)
![Configure the project to target Azure SQL Database](images/07-configure-database-project-02.jpg)

1. Save and close the configuration window.

1. Add a table to the Database Project.
![Add a table to the Database Project](images/08-add-table-01.jpg)
![Add a table to the Database Project](images/08-add-table-02.jpg)

1. Click File/Save All to save all changes.

1. Commit and sync changes.<br/>
![Commit and sync changes](images/09-commit-changes.jpg)

1. Enter a commit message and select Commit All and Sync.
![Enter a commit message and select Commit All and Sync](images/10-commit-and-sync.jpg)

1. Refresh the repository in Azure DevOps and verify that the project files were synchronized.
![Refresh the repository in Azure DevOps and verify that the project files were synchronized](images/11-check-devops-repo.jpg)

### Provision Azure SQL Database

Create an empty Azure SQL Database (single database).
Follow the steps at [Quickstart: Create an Azure SQL Database single database
](https://docs.microsoft.com/en-us/azure/azure-sql/database/single-database-create-quickstart)
Take note of resource group, server name, database name, admin username and password for later steps.

### Create a service connection in Azure DevOps for your Azure subscription

Create a service connection to access your Azure subscription.

1. Access the project's service connections and click "Create service connection".
![Access the project's service connections.](images/02-create-service-connection-01.jpg)

1. Select "Azure Resource Manager".<br/>
![Select "Azure Resource Manager"](images/02-create-service-connection-02.jpg)

1. Select "Service principal (automatic)".<br/>
![Select "Service principal (automatic)"](images/02-create-service-connection-03.jpg)

1. Configure the service connection.
   1. Select "Subscription" scope level.
   2. Select your subscription.
   3. Select the resource group where Azure SQL Database was provisioned.
   4. Enter "Azure" as the service connection name (the name will be used in the pipeline to reference the service connection).
![Configure the service connection](images/02-create-service-connection-04.jpg)

## Create the pipeline

1. Create a new pipeline in Azure DevOps.
![Create Pipeline](images/12-create-pipeline-01.jpg)

1. Select "Azure Repos Git" as the repository that contains the code.
![Select "Azure Repos Git"](images/12-create-pipeline-02.jpg)

1. Select the Sample Database Project as the Azure DevOps project containing the repository.
![Select the Sample Database Project](images/12-create-pipeline-03.jpg)

1. Select "Starter pipeline".
![Select "Starter pipeline"](images/12-create-pipeline-04.jpg)

1. Add variables for the Azure SQL Database configuration.
Add the following variables to your pipeline, based on the Azure SQL Database you created previously:

    Variable name | Content
    ------------- | --------
    sql_server | FQDN of the Azure SQL Database logical server
    sql_database | name of the Azure SQL Database
    sql_user | Azure SQL Database username
    sql_password | Azure SQL Database user password

    Repeat the steps below for all variables.

    ![Add variable](images/12-create-pipeline-05.jpg)<br/>
    ![Add variable](images/12-create-pipeline-06.jpg)<br/>
    ![Add variable](images/12-create-pipeline-07.jpg)

6. Change the pipeline code to the following:
    ``` yaml
    # Starter pipeline
    # Start with a minimal pipeline that you can customize to build and deploy your code.
    # Add steps that build, run tests, deploy, and more:
    # https://aka.ms/yaml

    trigger:
    - master

    pool:
    vmImage: 'windows-latest'

    steps:
    - task: VSBuild@1
    inputs:
        solution: '**\*.sln'

    - task: CopyFiles@2
    inputs:
        Contents: '**/*.dacpac'
        TargetFolder: '$(build.artifactstagingdirectory)'

    - task: SqlAzureDacpacDeployment@1
    inputs:
        azureSubscription: 'Azure'
        AuthenticationType: 'server'
        ServerName: '$(sql_server)'
        DatabaseName: '$(sql_database)'
        SqlUsername: '$(sql_user)'
        SqlPassword: '$(sql_password)'
        deployType: 'DacpacTask'
        DeploymentAction: 'Publish'
        DacpacFile: '$(build.artifactstagingdirectory)/Database1/Database1/bin/Debug/Database1.dacpac'
        IpDetectionMethod: 'AutoDetect'
    ```

7. Save and run the pipeline
    ![Save and run the pipeline](images/12-create-pipeline-08.jpg)
    ![Save and run the pipeline](images/12-create-pipeline-09.jpg)
    The pipeline will begin execution
    ![Pipeline execution](images/13-pipeline-execution.jpg)

8. After the pipeline completes, inspect the database schema to verify that the table you created in the database project has been created.
![Check database schema](images/14-check-database-schema.jpg)


### Success Criteria

1. You should understand why DataOps is important and the basic components.
2. 

[Back](challenge00.md) - [Home](../readme.md) - [Next](challenge02.md)