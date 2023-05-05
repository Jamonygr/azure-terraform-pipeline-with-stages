#Azure Terraform Pipeline with 2 Stages: Plan and Apply
This repository contains a Terraform configuration and an Azure DevOps pipeline for managing Azure infrastructure as code using the Terraform AzureRM provider. The pipeline is designed with two stages: Plan and Apply, which streamline the process of provisioning and managing Azure resources.

Overview
The Terraform Azure DevOps pipeline automates the process of creating, updating, or deleting Azure resources based on the provided Terraform configuration file. It ensures that the desired infrastructure is provisioned according to the defined configuration while minimizing human intervention and potential errors.

Stage 1: Terraform Init and Plan
This stage initializes the Terraform backend and generates an execution plan. The execution plan is a summary of the changes that Terraform will apply to the infrastructure. The stage includes the following jobs:

Install Terraform: Installs the latest version of Terraform, or the specified version if provided.
Checkout repository: Retrieves the source code from the repository.
Terraform Init: Initializes the Terraform backend, which includes downloading the required provider plugins and setting up the remote backend for storing the Terraform state.
Terraform Validate: Validates the Terraform configuration files to ensure they are syntactically correct and internally consistent.
Terraform Plan: Generates an execution plan, showing the changes that will be made to the infrastructure.
Publish Artifact: tfplan: Saves the execution plan as a pipeline artifact for use in the next stage.
Stage 2: Terraform Apply
This stage applies the generated execution plan to create, update, or delete the desired infrastructure. The stage includes the following jobs:

Install Terraform: Installs the latest version of Terraform, or the specified version if provided.
Checkout repository: Retrieves the source code from the repository.
Download Artifact: tfplan: Downloads the execution plan artifact from the previous stage.
Terraform Init: Re-initializes the Terraform backend, ensuring it is up-to-date.
Terraform Apply: Applies the execution plan, making the necessary changes to the infrastructure based on the plan.
Prerequisites
A Terraform configuration file in your repository.
An Azure DevOps project with a build pipeline configured.
An Azure subscription and a Service Principal with sufficient permissions to create, modify, and delete resources in the subscription.
Usage
Fork or clone this repository.
Add your Terraform configuration file to the repository.
Configure the necessary variables in your Azure DevOps build pipeline:
serviceName: The name of the Azure DevOps Service Principal.
remoteStateContainer: The name of the Azure Storage container where Terraform state files will be stored.
storageAccessKey: The access key for the Azure Storage account where the Terraform state files will be stored.
Commit your Terraform configuration file to the repository.
Run the build pipeline to create, update, or delete infrastructure as specified in your Terraform configuration file.
Notes
This pipeline assumes that you are using Azure Blob Storage for remote state management. If you are using a different backend, you will need to adjust the pipeline accordingly.
The pipeline uses the latest version of Terraform. If you need a specific version, change the terraformVersion input in the TerraformInstaller@0 tasks.
This pipeline uses the AzureRM provider for Terraform. If you are using a different provider, you will need to adjust the pipeline accordingly.
Contributing
If you would like to contribute to this repository, please follow these steps:

Fork the repository.
Create a new branch with a descriptive name.
Make your changes and commit them
