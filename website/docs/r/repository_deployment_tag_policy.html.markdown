---
layout: "github"
page_title: "GitHub: github_repository_deployment_tag_policy"
description: |-
  Creates and manages deployment tag policies
---

# github_repository_deployment_tag_policy

This resource allows you to create and manage deployment tag policies.


## Example Usage

```hcl
resource "github_repository_environment" "env" {
  repository  = "my_repo"
  environment = "my_env"
  deployment_branch_policy {
    protected_branches     = false
    custom_branch_policies = true
  }
}

resource "github_repository_deployment_tag_policy" "foo" {
  depends_on = [github_repository_environment.env]

  repository       = "my_repo"
  environment_name = "my_env"
  name             = "foo"
}
```


## Argument Reference

The following arguments are supported:

* `repository` - (Required) The repository to create the policy in.

* `environment_name` - (Required) The name of the environment. This environment must have `deployment_tag_policy.custom_tag_policies` set to true or a 404 error will be thrown.

* `name` - (Required) The name pattern that branches must match in order to deploy to the environment.

## Attributes Reference

The following additional attributes are exported:

* `id` - The ID of the deployment tag policy.

## Import

```
$ terraform import github_repository_deployment_tag_policy.foo repo:env:id
```
