# Azure Terraform Pipeline with 2 Stages: Plan and Apply

This README provides details about the Azure DevOps Terraform pipeline with two stages: Plan and Apply.

## Overview

This pipeline is designed specifically for Azure DevOps and uses the following stages:

1. **Terraform Init and Plan**: Initialize Terraform and generate an execution plan.
2. **Terraform Apply**: Apply the generated execution plan to create or modify the infrastructure.

## Features

- Utilizes Azure DevOps YAML pipelines
- Separates the Terraform planning and applying stages
- Validates the Terraform configuration before planning
- Publishes the Terraform plan as an artifact for later use
- Runs on an Ubuntu-Latest virtual machine image

## Requirements

- Azure DevOps account
- Azure Service Principal for authentication
- Azure Storage Account for storing Terraform remote state
- Terraform configuration files in the repository
- Install the [Terraform Microsoft DevLabs Extension](https://marketplace.visualstudio.com/items?itemName=ms-devlabs.custom-terraform-tasks&targetId=38d1a6f2-5cfa-416a-b5ca-23dcd7206c35&utm_source=vstsproduct&utm_medium=ExtHubManageList) from the Azure DevOps Marketplace

## Pipeline Stages

### 1. Terraform Init and Plan

This stage initializes Terraform, validates the configuration, generates an execution plan, and publishes it as an artifact. The following tasks are performed:

- Install the latest version of Terraform
- Checkout the repository
- Initialize Terraform with the `-reconfigure` option
- Validate the Terraform configuration
- Generate a Terraform plan
- Publish the Terraform plan as an artifact

### 2. Terraform Apply

This stage applies the previously generated Terraform plan to create or modify the infrastructure. The following tasks are performed:

- Install the latest version of Terraform
- Checkout the repository
- Download the Terraform plan artifact
- Initialize Terraform with the `-reconfigure` option
- Apply the Terraform plan with the `-auto-approve` and `-input=false` options

## Nodes

The pipeline uses the `ubuntu-latest` virtual machine image as its build agent. This image provides a Linux-based environment for running the pipeline tasks.

