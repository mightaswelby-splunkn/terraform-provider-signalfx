---
layout: "signalfx"
page_title: "SignalFx: signalfx_gcp_integration"
sidebar_current: "docs-signalfx-resource-gcp-integration"
description: |-
  Allows Terraform to create and manage SignalFx GCP Integrations
---

# Resource: signalfx_gcp_integration

SignalFx GCP Integration

~> **NOTE** When managing integrations use a session token for an administrator to authenticate the SignalFx provider. See [Operations that require a session token for an administrator].(https://dev.splunk.com/observability/docs/administration/authtokens#Operations-that-require-a-session-token-for-an-administrator). Otherwise you'll receive a 4xx error.

## Example Usage

```tf
resource "signalfx_gcp_integration" "gcp_myteam" {
  name      = "GCP - My Team"
  enabled   = true
  poll_rate = 300
  services  = ["compute"]
  project_service_keys {
    project_id  = "gcp_project_id_1"
    project_key = "${file("/path/to/gcp_credentials_1.json")}"
  }
  project_service_keys {
    project_id  = "gcp_project_id_2"
    project_key = "${file("/path/to/gcp_credentials_2.json")}"
  }
}
```

## Argument Reference

* `name` - (Required) Name of the integration.
* `enabled` - (Required) Whether the integration is enabled.
* `poll_rate` - (Optional) GCP integration poll rate (in seconds). Value between `60` and `600`. Default: `300`.
* `services` - (Optional) GCP service metrics to import. Can be an empty list, or not included, to import 'All services'. See the documentation for [Creating Integrations](https://developers.signalfx.com/integrations_reference.html#operation/Create%20Integration) for valid values.
* `project_service_keys` - (Required) GCP projects to add.
* `whilelist` - (Optional) [Compute Metadata Whitelist](https://docs.signalfx.com/en/latest/integrations/google-cloud-platform.html#compute-engine-instance).

## Attributes Reference

In a addition to all arguments above, the following attributes are exported:

* `id` - The ID of the integration.
