# Azure Umanis Resource Group

[![Build Status](https://dev.azure.com/umanis-consulting/terraform/_apis/build/status/mod_azu_resource_group?repoName=mod_azu_resource_group&branchName=master)](https://dev.azure.com/umanis-consulting/terraform/_build/latest?definitionId=3&repoName=mod_azu_resource_group&branchName=master) [![Unilicence](https://img.shields.io/badge/licence-The%20Unilicence-green)](LICENCE)


Common Azure terraform module to create a Resource Group

## Naming
Resource naming is based on the Microsoft CAF naming convention best practices. Custom naming is available by setting the parameter `custom_name`. We rely on the official Terraform Azure CAF naming provider to generate resource names when available.

## Usage
```hcl

module "umanis_tagging" {
  source = "Umanis/tags/azurerm"

  location          = "France Central"
  client            = "XY2"
  project           = "1234"
  budget            = "FE4567"
  rgpd_personal     = true
  rgpd_confidential = false
}

module "umanis_naming" {
  source = "Umanis/naming/azurerm"

  location    = "France Central"
  client      = "XY2"
  project     = "1234"
  area        = 1
  environment = "tst"
}

module "umanis_resource_group" {
  source = "Umanis/resource-group/azurerm"

  tags         = module.umanis_tagging.tags
  location     = "France Central"
  description  = "Test resource group"
  caf_prefixes = module.umanis_naming.resource_group_prefixes
}


```
<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 0.15.0 |
| <a name="requirement_azurecaf"></a> [azurecaf](#requirement\_azurecaf) | >= 1.2.5 |
| <a name="requirement_azurerm"></a> [azurerm](#requirement\_azurerm) | >=2.62.0 |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_location"></a> [location](#input\_location) | Azure region to use for deployment. | `string` | n/a | yes |
| <a name="input_tags"></a> [tags](#input\_tags) | Resource group tags. | `map(string)` | n/a | yes |
| <a name="input_caf_prefixes"></a> [caf\_prefixes](#input\_caf\_prefixes) | Prefixes to use for caf naming. | `list(string)` | `[]` | no |
| <a name="input_custom_name"></a> [custom\_name](#input\_custom\_name) | If defined, resource group custom name. | `string` | `""` | no |
| <a name="input_description"></a> [description](#input\_description) | Resource group description. | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_id"></a> [id](#output\_id) | Resource group id |
| <a name="output_location"></a> [location](#output\_location) | Resource group location |
| <a name="output_name"></a> [name](#output\_name) | Resource group name |
<!-- END_TF_DOCS -->

## Related documentation

Terraform Azure resource group documentation: [https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group](https://registry.terraform.io/providers/hashicorp/azurerm/latest/docs/resources/resource_group)

Terraform Azure CAF Naming documentation: [https://registry.terraform.io/providers/aztfmod/azurecaf/latest/docs/resources/azurecaf_name](https://registry.terraform.io/providers/aztfmod/azurecaf/latest/docs/resources/azurecaf_name)

