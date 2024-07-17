# Terraform-google-vm
# Terraform Google Cloud vm Module
## Table of Contents

## Table of Contents
- [Introduction](#introduction)
- [Usage](#usage)
- [Module Inputs](#module-inputs)
- [Module Outputs](#module-outputs)
- [Authors](#authors)
- [License](#license)

## Introduction
This project deploys a Google Cloud infrastructure using Terraform to create vm .

## Usage

To use this module, you should have Terraform installed and configured for GCP. This module provides the necessary Terraform configuration for creating GCP resources, and you can customize the inputs as needed. Below is an example of how to use this module:
# Example: compute_instance

```hcl

module "compute_instance" {
  source                 = "https://github.com/yadavprakash/terraform-gcp-vm.git"
  name                   = "dev"
  environment            = "test"
  instance_count         = 1
  instance_tags          = ["foo", "bar"]
  machine_type           = "e2-small"
  image                  = "ubuntu-2204-jammy-v20230908"
  gcp_zone               = "asia-northeast1-a"
  service_account_scopes = ["cloud-platform"]
  subnetwork             = module.subnet.subnet_id

  # Enable public IP only if enable_public_ip is true
  enable_public_ip = true
  metadata = {
    ssh-keys = <<EOF
      test:ssh-rsa AAAAB3NzaC1yc
    EOF
  }
}
```

This example demonstrates how to create various GCP resources using the provided modules. Adjust the input values to suit your specific requirements.

## Module Inputs

- `name`: The name of the application or resource.
- `environment`: The environment in which the resource exists.
- `label_order`: The order in which labels should be applied.
- `business_unit`: The business unit associated with the application.
- `attributes`: Additional attributes to add to the labels.
- `extra_tags`: Extra tags to associate with the resource.

## Module Outputs
- This module currently does not provide any outputs.

# Examples
For detailed examples on how to use this module, please refer to the [example](https://github.com/yadavprakash/terraform-gcp-vm/tree/master/_example) directory within this repository.

## Authors
Your Name
Replace '[License Name]' and '[Your Name]' with the appropriate license and your information. Feel free to expand this README with additional details or usage instructions as needed for your specific use case.

## License
This project is licensed under the MIT License - see the [LICENSE](https://github.com/yadavprakash/terraform-gcp-vm/blob/master/LICENSE) file for details.



<!-- BEGIN_TF_DOCS -->
## Requirements

| Name | Version |
|------|---------|
| <a name="requirement_terraform"></a> [terraform](#requirement\_terraform) | >= 1.6.6 |
| <a name="requirement_google"></a> [google](#requirement\_google) | >= 3.50, < 5.13.0 |

## Providers

| Name | Version |
|------|---------|
| <a name="provider_google"></a> [google](#provider\_google) | >= 3.50, < 5.13.0 |

## Modules

| Name | Source | Version |
|------|--------|---------|
| <a name="module_labels"></a> [labels](#module\_labels) | git::git@github.com:yadavprakash/terraform-gcp-labels.git | v1.0.0 |

## Resources

| Name | Type |
|------|------|
| [google_compute_instance.default](https://registry.terraform.io/providers/hashicorp/google/latest/docs/resources/compute_instance) | resource |
| [google_client_config.current](https://registry.terraform.io/providers/hashicorp/google/latest/docs/data-sources/client_config) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_allow_stopping_for_update"></a> [allow\_stopping\_for\_update](#input\_allow\_stopping\_for\_update) | must be set to true or your instance must have a desired\_status of TERMINATED in order to update this field. | `bool` | `true` | no |
| <a name="input_create_instances"></a> [create\_instances](#input\_create\_instances) | Toggle to determine whether instances should be created or not. Set to 'true' to create instances, 'false' to skip instance creation. | `bool` | `true` | no |
| <a name="input_enable_public_ip"></a> [enable\_public\_ip](#input\_enable\_public\_ip) | Predefined enable\_public\_ip  address for the instance. | `bool` | `false` | no |
| <a name="input_environment"></a> [environment](#input\_environment) | Environment (e.g. `prod`, `dev`, `staging`). | `string` | `""` | no |
| <a name="input_gcp_zone"></a> [gcp\_zone](#input\_gcp\_zone) | The GCP zone to create resources in | `string` | `""` | no |
| <a name="input_image"></a> [image](#input\_image) | Source image family. If neither source\_image nor source\_image\_family is specified, defaults to the latest public CentOS image. | `string` | `"ubuntu-2204-jammy-v20230908"` | no |
| <a name="input_instance_count"></a> [instance\_count](#input\_instance\_count) | The number of instances to create. | `number` | `1` | no |
| <a name="input_instance_tags"></a> [instance\_tags](#input\_instance\_tags) | Network tags, provided as a list | `list(string)` | `[]` | no |
| <a name="input_label_order"></a> [label\_order](#input\_label\_order) | Label order, e.g. sequence of application name and environment `name`,`environment`,'attribute' [`webserver`,`qa`,`devops`,`public`,] . | `list(any)` | <pre>[<br>  "name",<br>  "environment"<br>]</pre> | no |
| <a name="input_machine_type"></a> [machine\_type](#input\_machine\_type) | Machine type to create, e.g. n1-standard-1 | `string` | `""` | no |
| <a name="input_managedby"></a> [managedby](#input\_managedby) | ManagedBy'yadavprakash'. | `string` | `"yadavprakash"` | no |
| <a name="input_metadata"></a> [metadata](#input\_metadata) | Metadata, provided as a map | `map(string)` | `{}` | no |
| <a name="input_metadata_startup_script"></a> [metadata\_startup\_script](#input\_metadata\_startup\_script) | User startup script to run when instances spin up | `string` | `""` | no |
| <a name="input_name"></a> [name](#input\_name) | Name of the resource. Provided by the client when the resource is created. | `string` | `""` | no |
| <a name="input_repository"></a> [repository](#input\_repository) | Terraform current module repo | `string` | `""` | no |
| <a name="input_service_account_email"></a> [service\_account\_email](#input\_service\_account\_email) | The service account e-mail address. | `string` | `""` | no |
| <a name="input_service_account_scopes"></a> [service\_account\_scopes](#input\_service\_account\_scopes) | A list of service scopes. | `list(string)` | `[]` | no |
| <a name="input_subnetwork"></a> [subnetwork](#input\_subnetwork) | Subnet to deploy to. Only one of network or subnetwork should be specified. | `string` | `""` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_cpu_platform"></a> [cpu\_platform](#output\_cpu\_platform) | The CPU platform used by this instance. |
| <a name="output_current_status"></a> [current\_status](#output\_current\_status) | The current status of the instance. |
| <a name="output_instance_count"></a> [instance\_count](#output\_instance\_count) | The value of the instance\_count variable. |
| <a name="output_instance_count_output"></a> [instance\_count\_output](#output\_instance\_count\_output) | The value of the instance\_count variable. |
| <a name="output_instance_id"></a> [instance\_id](#output\_instance\_id) | The server-assigned unique identifier of this instance. |
| <a name="output_label_fingerprint"></a> [label\_fingerprint](#output\_label\_fingerprint) | The unique fingerprint of the labels. |
| <a name="output_metadata_fingerprint"></a> [metadata\_fingerprint](#output\_metadata\_fingerprint) | The unique fingerprint of the metadata. |
| <a name="output_name"></a> [name](#output\_name) | The name  of the instance. |
| <a name="output_self_link"></a> [self\_link](#output\_self\_link) | The URI of the created resource. |
| <a name="output_tags_fingerprint"></a> [tags\_fingerprint](#output\_tags\_fingerprint) | The unique fingerprint of the tags. |
<!-- END_TF_DOCS -->