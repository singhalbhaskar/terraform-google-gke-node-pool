# terraform-google-gke-node-pool

## Description
### Tagline
This is an auto-generated module.

### Detailed
This module was generated from [terraform-google-module-template](https://github.com/terraform-google-modules/terraform-google-module-template/), which by default generates a module that simply creates a GCS bucket. As the module develops, this README should be updated.

The resources/services/activations/deletions that this module will create/trigger are:

- Create a GCS bucket with the provided name

### PreDeploy
To deploy this blueprint you must have an active billing account and billing permissions.

## Architecture
![alt text for diagram](https://www.link-to-architecture-diagram.com)
1. Architecture description step no. 1
2. Architecture description step no. 2
3. Architecture description step no. N

## Documentation
- [Hosting a Static Website](https://cloud.google.com/storage/docs/hosting-static-website)

## Deployment Duration
Configuration: X mins
Deployment: Y mins

## Cost
[Blueprint cost details](https://cloud.google.com/products/calculator?id=02fb0c45-cc29-4567-8cc6-f72ac9024add)

## Usage

Basic usage of this module is as follows:

```hcl
module "gke_node_pool" {
  source  = "terraform-google-modules/gke-node-pool/google"
  version = "~> 0.1"

  project_id  = "<PROJECT ID>"
  bucket_name = "gcs-test-bucket"
}
```

Functional examples are included in the
[examples](./examples/) directory.

<!-- BEGINNING OF PRE-COMMIT-TERRAFORM DOCS HOOK -->
## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| additional\_networks | Additional network interface details for GKE, if any. Providing additional networks adds additional node networks to the node pool | <pre>list(object({<br>    network            = string<br>    subnetwork         = string<br>    subnetwork_project = string<br>    network_ip         = string<br>    nic_type           = string<br>    stack_type         = string<br>    queue_count        = number<br>    access_config = list(object({<br>      nat_ip       = string<br>      network_tier = string<br>    }))<br>    ipv6_access_config = list(object({<br>      network_tier = string<br>    }))<br>    alias_ip_range = list(object({<br>      ip_cidr_range         = string<br>      subnetwork_range_name = string<br>    }))<br>  }))</pre> | `[]` | no |
| auto\_upgrade | Whether the nodes will be automatically upgraded. | `bool` | `false` | no |
| autoscaling\_total\_max\_nodes | Total maximum number of nodes in the NodePool. | `number` | `1000` | no |
| autoscaling\_total\_min\_nodes | Total minimum number of nodes in the NodePool. | `number` | `0` | no |
| cluster\_id | projects/{{project}}/locations/{{location}}/clusters/{{cluster}} | `string` | n/a | yes |
| compact\_placement | DEPRECATED: Use `placement_policy` | `bool` | `null` | no |
| disk\_size\_gb | Size of disk for each node. | `number` | `100` | no |
| disk\_type | Disk type for each node. | `string` | `null` | no |
| enable\_gcfs | Enable the Google Container Filesystem (GCFS). See [restrictions](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/container_cluster#gcfs_config). | `bool` | `false` | no |
| enable\_secure\_boot | Enable secure boot for the nodes.  Keep enabled unless custom kernel modules need to be loaded. See [here](https://cloud.google.com/compute/shielded-vm/docs/shielded-vm#secure-boot) for more info. | `bool` | `true` | no |
| gke\_version | GKE version | `string` | n/a | yes |
| guest\_accelerator | List of the type and count of accelerator cards attached to the instance. | <pre>list(object({<br>    type  = optional(string)<br>    count = optional(number, 0)<br>    gpu_driver_installation_config = optional(list(object({<br>      gpu_driver_version = string<br>    })))<br>    gpu_partition_size = optional(string)<br>    gpu_sharing_config = optional(list(object({<br>      gpu_sharing_strategy       = optional(string)<br>      max_shared_clients_per_gpu = optional(number)<br>    })))<br>  }))</pre> | `null` | no |
| host\_maintenance\_interval | Specifies the frequency of planned maintenance events. | `string` | `""` | no |
| image\_type | The default image type used by NAP once a new node pool is being created. Use either COS\_CONTAINERD or UBUNTU\_CONTAINERD. | `string` | `"COS_CONTAINERD"` | no |
| initial\_node\_count | The initial number of nodes for the pool. In regional clusters, this is the number of nodes per zone. Changing this setting after node pool creation will not make any effect. It cannot be set with static\_node\_count and must be set to a value between autoscaling\_total\_min\_nodes and autoscaling\_total\_max\_nodes. | `number` | `null` | no |
| kubernetes\_labels | Kubernetes labels to be applied to each node in the node group. Key-value pairs. <br>(The `kubernetes.io/` and `k8s.io/` prefixes are reserved by Kubernetes Core components and cannot be specified) | `map(string)` | `null` | no |
| labels | GCE resource labels to be applied to resources. Key-value pairs. | `map(string)` | n/a | yes |
| local\_ssd\_count\_ephemeral\_storage | The number of local SSDs to attach to each node to back ephemeral storage.<br>Uses NVMe interfaces.  Must be supported by `machine_type`.<br>When set to null,  default value either is [set based on machine\_type](https://cloud.google.com/compute/docs/disks/local-ssd#choose_number_local_ssds) or GKE decides about default value.<br>[See above](#local-ssd-storage) for more info. | `number` | `null` | no |
| local\_ssd\_count\_nvme\_block | The number of local SSDs to attach to each node to back block storage.<br>Uses NVMe interfaces.  Must be supported by `machine_type`.<br>When set to null,  default value either is [set based on machine\_type](https://cloud.google.com/compute/docs/disks/local-ssd#choose_number_local_ssds) or GKE decides about default value.<br>[See above](#local-ssd-storage) for more info. | `number` | `null` | no |
| machine\_type | The name of a Google Compute Engine machine type. | `string` | `"c2-standard-60"` | no |
| name | The name of the node pool. If not set, automatically populated by machine type and module id (unique blueprint-wide) as suffix.<br>If setting manually, ensure a unique value across all gke-node-pools. | `string` | `null` | no |
| node\_count | The number of nodes in the node pool | `number` | n/a | yes |
| placement\_policy | Group placement policy to use for the node pool's nodes. `COMPACT` is the only supported value for `type` currently. `name` is the name of the placement policy.<br>It is assumed that the specified policy exists. To create a placement policy refer to https://cloud.google.com/sdk/gcloud/reference/compute/resource-policies/create/group-placement.<br>Note: Placement policies have the [following](https://cloud.google.com/compute/docs/instances/placement-policies-overview#restrictions-compact-policies) restrictions. | <pre>object({<br>    policy_type = string<br>    policy_name = optional(string)<br>  })</pre> | <pre>{<br>  "policy_type": ""<br>}</pre> | no |
| placement\_policy\_name | Toolkit deployment variable: placement\_policy\_name | `string` | n/a | yes |
| project\_id | The project ID to host the cluster in. | `string` | n/a | yes |
| reservation | Toolkit deployment variable: reservation | `string` | n/a | yes |
| reservation\_affinity | Reservation resource to consume. When targeting SPECIFIC\_RESERVATION, specific\_reservations needs be specified.<br>Even though specific\_reservations is a list, only one reservation is allowed by the NodePool API.<br>It is assumed that the specified reservation exists and has available capacity.<br>For a shared reservation, specify the project\_id as well in which it was created.<br>To create a reservation refer to https://cloud.google.com/compute/docs/instances/reservations-single-project and https://cloud.google.com/compute/docs/instances/reservations-shared | <pre>object({<br>    consume_reservation_type = string<br>    specific_reservations = optional(list(object({<br>      name    = string<br>      project = optional(string)<br>    })))<br>  })</pre> | <pre>{<br>  "consume_reservation_type": "NO_RESERVATION",<br>  "specific_reservations": []<br>}</pre> | no |
| reservation\_block | Toolkit deployment variable: reservation\_block | `string` | n/a | yes |
| service\_account | DEPRECATED: use service\_account\_email and scopes. | <pre>object({<br>    email  = string,<br>    scopes = set(string)<br>  })</pre> | `null` | no |
| service\_account\_email | Service account e-mail address to use with the node pool | `string` | `null` | no |
| service\_account\_scopes | Scopes to to use with the node pool. | `set(string)` | <pre>[<br>  "https://www.googleapis.com/auth/cloud-platform"<br>]</pre> | no |
| spot | Provision VMs using discounted Spot pricing, allowing for preemption | `bool` | `false` | no |
| taints | Taints to be applied to the system node pool. | <pre>list(object({<br>    key    = string<br>    value  = any<br>    effect = string<br>  }))</pre> | <pre>[<br>  {<br>    "effect": "NO_SCHEDULE",<br>    "key": "user-workload",<br>    "value": true<br>  }<br>]</pre> | no |
| threads\_per\_core | Sets the number of threads per physical core. By setting threads\_per\_core<br>to 2, Simultaneous Multithreading (SMT) is enabled extending the total number<br>of virtual cores. For example, a machine of type c2-standard-60 will have 60<br>virtual cores with threads\_per\_core equal to 2. With threads\_per\_core equal<br>to 1 (SMT turned off), only the 30 physical cores will be available on the VM.<br><br>The default value of \"0\" will turn off SMT for supported machine types, and<br>will fall back to GCE defaults for unsupported machine types (t2d, shared-core<br>instances, or instances with less than 2 vCPU).<br><br>Disabling SMT can be more performant in many HPC workloads, therefore it is<br>disabled by default where compatible.<br><br>null = SMT configuration will use the GCE defaults for the machine type<br>0 = SMT will be disabled where compatible (default)<br>1 = SMT will always be disabled (will fail on incompatible machine types)<br>2 = SMT will always be enabled (will fail on incompatible machine types) | `number` | `0` | no |
| timeout\_create | Timeout for creating a node pool | `string` | `null` | no |
| timeout\_update | Timeout for updating a node pool | `string` | `null` | no |
| total\_max\_nodes | DEPRECATED: Use autoscaling\_total\_max\_nodes. | `number` | `null` | no |
| total\_min\_nodes | DEPRECATED: Use autoscaling\_total\_min\_nodes. | `number` | `null` | no |
| zone | A zone | `string` | n/a | yes |

## Outputs

| Name | Description |
|------|-------------|
| node\_pool\_name | Name of the node pool. |

<!-- END OF PRE-COMMIT-TERRAFORM DOCS HOOK -->

## Requirements

These sections describe requirements for using this module.

### Software

The following dependencies must be available:

- [Terraform][terraform] v0.13
- [Terraform Provider for GCP][terraform-provider-gcp] plugin v3.0

### Service Account

A service account with the following roles must be used to provision
the resources of this module:

- Storage Admin: `roles/storage.admin`

The [Project Factory module][project-factory-module] and the
[IAM module][iam-module] may be used in combination to provision a
service account with the necessary roles applied.

### APIs

A project with the following APIs enabled must be used to host the
resources of this module:

- Google Cloud Storage JSON API: `storage-api.googleapis.com`

The [Project Factory module][project-factory-module] can be used to
provision a project with the necessary APIs enabled.

## Contributing

Refer to the [contribution guidelines](./CONTRIBUTING.md) for
information on contributing to this module.

[iam-module]: https://registry.terraform.io/modules/terraform-google-modules/iam/google
[project-factory-module]: https://registry.terraform.io/modules/terraform-google-modules/project-factory/google
[terraform-provider-gcp]: https://www.terraform.io/docs/providers/google/index.html
[terraform]: https://www.terraform.io/downloads.html

## Security Disclosures

Please see our [security disclosure process](./SECURITY.md).
