# What The Hack - DataOps
## Introduction
This intro level hack will help you get hands-on experience with building a Continuous Integration and Continuous Delivery pipeline for a Data Estate (ETL) project. We will be using the Azure DevOps Project and GitHub actions for build and release/deployment pipelines for Azure Data Factory, Azure SQL Database, Databricks and Cosmos DB.

This hack starts off by covering DataOps is, what problems it solves, and why DataOps Process is needed to simply the complexity of data analytics creation and operations. You will learn how to streamline and automate the analytics development lifecycle leveraing best practices from Agile development and CI/CD. DataOps helps overcome the hurdles and complexities and deliver analytics with speed and agility, without compromising on data quality. It derives inspiration from the practices of Lean Manufacturing, Agile and DevOps. 

This hack includes a optional [lecture presentation](Coach/Lectures.pptx) that features short presentations to introduce key topics associated with each challenge. It is recommended that the host present each short presentation before attendees kick off that challenge.

## Learning Objectives
In this hack you will solve a common challenge for companies automating their modern Data Warehouse platform. You will take a standard data warehouse architecture, automate the provisioning of the required services infrastructure, automate a CI build for the ETL process to Azure Data services.  

1. Build and Deploy Data Estate Infrastructure
1. Build SQL Data Pipeline Databricks. 
1. Deploy ADF Pipeline, SQL and Databricks


## Challenges
- Challenge 0: **[Pre-requisites - Ready, Set, GO!](Student/00-prereqs.md)**
   - Prepare your workstation to work with Azure, Docker containers, and AKS
- Challenge 1: **[Basic DevOps with SQL Database Project](Student/01-containers.md)**
   - Generate a VS data project from an existing schema
- Challenge 2: **[Place project under version control in Git](Student/02-acr.md)**
   - Discuss version control (centralized vs decentralized)
   - Discuss local vs remote
   - Discuss commits
- Challenge 3: **[Create Build and Release Pipeline](Student/03-k8sintro.md)**
   - Discuss build artifacts as Release candidate
   - Build once, deploy many
   - DACPAC handles deployment-time activities at deployment time rather than design time (update scripts)
   - Discuss Service Principals in Azure DevOps pipelines
   - Discuss Microsoft Hosted vs. Private Pipeline Agents
   - Call out specifically that Hosted agents can't see into private resources in Azure (Private vNet, ASE, ISE, SQL MI, etc)
   - Deploy new database to SQL MI   
- Challenge 4: **[Deploy new database to SQL MI](Student/04-k8sdeployment.md)**
   - Make a change
   - Discuss branching for isolation
   - Isolation versus Integration
   - Create branch in Git and checkout
   - Change something in SSMS and sync with VS
   - Save changes on branch
   - Commit changes to local branch
   - Push branch to remote repo
   - PR changes to Main and discuss Pull Requests
   - Trigger build and release 
- Challenge 5: **[DevOps with Data Bricks and Data Factory ](Student/05-scaling.md)**
   - Data Bricks and Data Factory development without DevOps
   - Configure Git repo with Data Factory
   - Discuss Git branching model in relation to Data Factory
   - Discuss PR back to Main in Data Factory
   - Discuss Publish (build) processin Data Factory
   - Setup hybrid manual and automated CI process for Data Factory in Azure build pipelines
   - Setup CD process for Data Factory in Azure release pipelines
   - Deploy to a data factory
   - Make a change on a branch
   - PR branch back to Main
   - Publish Main to Data Factory to kick off full CI/CD process   
- Challenge 6: **[CI with Data Bricks](Student/06-deploymongo.md)**
   - Configure DataBricks to use Git repo for Notebooks
   - Same repo as Data Factory
   - Discuss Git branching model in relation to Data Bricks
   - Discuss PR back to Main in Data Bricks
   - Add Data Bricks CI process to branch
   - Add Data Bricks to CI process on Main
- Challenge 7: **[CD with Data Bricks](Student/07-updaterollback.md)**
   - Add Data Bricks to CD process
   - Deploy Data Bricks
   - Make a change on a branch
   - PR change back to Main
   - Review full CI/CD process for Data Factory and Data Bricks

   
## Prerequisites

- Access to an Azure subscription with Owner access
   - If you don't have one, [Sign Up for Azure HERE](https://azure.microsoft.com/en-us/free/)
- [**Windows Subsystem for Linux (Windows 10-only)**](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
- [**Azure CLI**](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli)
   - (Windows-only) Install Azure CLI on Windows Subsystem for Linux
   - Update to the latest
   - Must be at least version 2.7.x
- Alternatively, you can use the [**Azure Cloud Shell**](https://shell.azure.com/)
- [**Visual Studio Code**](https://code.visualstudio.com/)

## Repository Contents
- `../Coach/Guides`
  - [Lecture presentation](Coach/Lectures.pptx) with short presentations to introduce each challenge.
- `../Coach/Solutions`
   - Example solutions to the challenges (If you're a student, don't cheat yourself out of an education!)
- `../Student/Resources`
   - Sample app code and sample templates to aid with challenges

## Contributors
- William H. Salazar