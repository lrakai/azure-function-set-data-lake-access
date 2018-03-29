# azure-function-set-data-lake-access

This project is inspired by [AWS CloudFormation custom resources](https://docs.aws.amazon.com/AWSCloudFormation/latest/UserGuide/template-custom-resources.html). 
With custom resources you can include any resource in your infrastructure templates, even resources not in AWS.
Azure Resource Manager (ARM) templates don't have an analogous resource type.
However, you can come close deploying an Azure Function that is set to run on startup.

This project demonstrates the approach of deploying a function in an ARM template and retrieve Azure credentials using Azure Key Vault.
The particular example uses the Azure function to set the permission of an Azure Data Lake Store that is created by the template.
It is not possible to set file permissions of the Azure Data Lake Store directly in the ARM template, so the Function is used to set permissions.


## Repo Organization

- `templates`: Includes arm templates for creating a key vault (`key-vault-template.json`), deploying a data lake and function to modify its permissions (`arm-template.json`), and a parent template to dynamically set the secureString parameter values from Azure Key Vault without a separate parameters file (`vault-parameters-template.json`).
- `SetADLSPermission`: Azure Function project to set the permission of the Data Lake Store. This project is deployed by `templates/arm-template.json`.