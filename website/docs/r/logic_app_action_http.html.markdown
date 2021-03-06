---
layout: "azurerm"
page_title: "Azure Resource Manager: azurerm_logic_app_action_http"
sidebar_current: "docs-azurerm-resource-logic-app-action-http"
description: |-
  Manages an HTTP Action within a Logic App Workflow
---

# azurerm_logic_app_action_http

Manages an HTTP Action within a Logic App Workflow

## Example Usage

```hcl
resource "azurerm_resource_group" "test" {
  name     = "workflow-resources"
  location = "East US"
}

resource "azurerm_logic_app_workflow" "test" {
  name = "workflow1"
  location = "${azurerm_resource_group.test.location}"
  resource_group_name = "${azurerm_resource_group.test.name}"
}

resource "azurerm_logic_app_action_http" "test" {
  name         = "webhook"
  logic_app_id = "${azurerm_logic_app_workflow.test.id}"
  method       = "GET"
  uri          = "http://example.com/some-webhook"
}
```

## Argument Reference

The following arguments are supported:

* `name` - (Required) Specifies the name of the HTTP Action to be created within the Logic App Workflow. Changing this forces a new resource to be created.

-> **NOTE:** This name must be unique across all Actions within the Logic App Workflow.

* `logic_app_id` - (Required) Specifies the ID of the Logic App Workflow. Changing this forces a new resource to be created.

* `method` - (Required) Specifies the HTTP Method which should be used for this HTTP Action. Possible values include `DELETE`, `GET`, `PATCH`, `POST` and `PUT`.

* `uri` - (Required) Specifies the URI which will be called when this HTTP Action is triggered.

* `body` - (Optional) Specifies the HTTP Body that should be sent to the `uri` when this HTTP Action is triggered.

* `headers` - (Optional) Specifies a Map of Key-Value Pairs that should be sent to the `uri` when this HTTP Action is triggered.

## Attributes Reference

The following attributes are exported:

* `id` - The ID of the HTTP Action within the Logic App Workflow.

## Import

Logic App HTTP Actions can be imported using the `resource id`, e.g.

```shell
terraform import azurerm_logic_app_action_http.webhook1 /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mygroup1/providers/Microsoft.Logic/workflows/workflow1/actions/webhook1
```

-> **NOTE:** This ID is unique to Terraform and doesn't directly match to any other resource. To compose this ID, you can take the ID Logic App Workflow and append `/actions/{name of the action}`.
