---
layout: "azurerm"
page_title: "Azure Resource Manager: azurerm_api_management_product_group"
sidebar_current: "docs-azurerm-resource-api-management-product-group"
description: |-
  Manages an API Management Product Assignment to a Group.
---

# azurerm_api_management_product_group

Manages an API Management Product Assignment to a Group.

## Example Usage

```hcl
data "azurerm_api_management" "example" {
  name                = "example-api"
  resource_group_name = "example-resources"
}

data "azurerm_api_management_product" "example" {
  product_id          = "my-product"
  api_management_name = "${data.azurerm_api_management.example.name}"
  resource_group_name = "${data.azurerm_api_management.example.resource_group_name}"
}

data "azurerm_api_management_group" "example" {
  name                = "my-group"
  api_management_name = "${data.azurerm_api_management.example.name}"
  resource_group_name = "${data.azurerm_api_management.example.resource_group_name}"
}

resource "azurerm_api_management_group_user" "example" {
  user_id             = "${data.azurerm_api_management_user.example.id}"
  group_name          = "${data.azurerm_api_management_group.example.name}"
  api_management_name = "${data.azurerm_api_management.example.name}"
  resource_group_name = "${data.azurerm_api_management.example.resource_group_name}"
}
```

## Argument Reference

The following arguments are supported:

* `user_id` - (Required) The ID of the API Management User which should be assigned to this API Management Group. Changing this forces a new resource to be created.

* `group_name` - (Required) The Name of the API Management Group within the API Management Service. Changing this forces a new resource to be created.

* `api_management_name` - (Required) The name of the API Management Service. Changing this forces a new resource to be created.

* `resource_group_name` - (Required) The name of the Resource Group in which the API Management Service exists. Changing this forces a new resource to be created.

## Attributes Reference

In addition to all arguments above, the following attributes are exported:

* `id` - The ID of the API Management Product Group.

## Import

API Management Product Groups can be imported using the `resource id`, e.g.

```shell
terraform import azurerm_api_management_product_group.example /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/group1/providers/Microsoft.ApiManagement/service/service1/products/exampleId/groups/groupId
```
