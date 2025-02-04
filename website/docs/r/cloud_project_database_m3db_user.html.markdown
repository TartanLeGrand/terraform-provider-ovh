---
layout: "ovh"
page_title: "OVH: cloud_project_database_m3db_user"
sidebar_current: "docs-ovh-resource-cloud-project-database-m3db-user"
description: |-
  Creates an user for a M3DB cluster associated with a public cloud project.
---

# ovh_cloud_project_database_m3db_user

Creates an user for a M3DB cluster associated with a public cloud project.

## Example Usage

```hcl
data "ovh_cloud_project_database" "m3db" {
  service_name  = "XXX"
  engine        = "m3db"
  id            = "ZZZ"
}

resource "ovh_cloud_project_database_m3db_user" "user" {
  service_name  = data.ovh_cloud_project_database.m3db.service_name
  cluster_id    = data.ovh_cloud_project_database.m3db.id
  group         = "mygroup"
  name          = "johndoe"
}
```

## Argument Reference

The following arguments are supported:

* `service_name` - (Required, Forces new resource) The id of the public cloud project. If omitted,
  the `OVH_CLOUD_PROJECT_SERVICE` environment variable is used.

* `cluster_id` - (Required, Forces new resource) Cluster ID.

* `group` - (Optional) Group of the user:

* `name` - (Required, Forces new resource) Name of the user.

## Attributes Reference

The following attributes are exported:

* `cluster_id` - See Argument Reference above.
* `created_at` - Date of the creation of the user.
* `id` - ID of the user.
* `group` - See Argument Reference above.
* `name` - See Argument Reference above.
* `password` - (Sensitive) Password of the user.
* `service_name` - See Argument Reference above.
* `status` - Current status of the user.

## Timeouts

```hcl
resource "ovh_cloud_project_database_m3db_user" "user" {
  # ...

  timeouts {
    create = "1h"
    update = "45m"
    delete = "50s"
  }
}
```
* `create` - (Default 20m)
* `update` - (Default 20m)
* `delete` - (Default 20m)

## Import

OVHcloud Managed M3DB clusters users can be imported using the `service_name`, `cluster_id` and `id` of the user, separated by "/" E.g.,

```bash
$ terraform import ovh_cloud_project_database_m3db_user.my_user service_name/cluster_id/id
```