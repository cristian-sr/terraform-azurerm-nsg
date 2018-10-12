[![Build Status](https://jenkins-terraform.mesosphere.com/service/dcos-terraform-jenkins/job/dcos-terraform/job/terraform-azurerm-nsg/job/master/badge/icon)](https://jenkins-terraform.mesosphere.com/service/dcos-terraform-jenkins/job/dcos-terraform/job/terraform-azurerm-nsg/job/master/)
azurerm nsg
===========
The module creates DC/OS Network Security Groups per DC/OS role on AzureRM.

EXAMPLE
-------

```hcl
module "dcos-security-groups" {
  source  = "dcos-terraform/nsg/azurerm"
  version = "~> 0.1"

  resource_group_name = "test"
  location            = "West US"
  subnet_range        = "10.0.10.0/24"
  admin_ips           = ["1.2.3.4/32"]
}
```


## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-----:|:-----:|
| admin_ips | List of CIDR admin IPs | list | - | yes |
| cluster_name | Cluster Name | string | - | yes |
| hostname_format | Format the hostname inputs are index+1, region, cluster_name | string | `nsg-%[1]d-%[2]s` | no |
| location | location | string | - | yes |
| public_agents_additional_ports | List of additional ports allowed for public access on public agents (80 and 443 open by default) | list | `<list>` | no |
| public_agents_ips | List of ips allowed access to public agents. admin_ips are joined to this list | list | `<list>` | no |
| resource_group_name | resource group name | string | - | yes |
| subnet_range | Private IP space to be used in CIDR format | string | - | yes |
| tags | Add custom tags to all resources | map | `<map>` | no |

## Outputs

| Name | Description |
|------|-------------|
| bootstrap.nsg_id | Network Security Group ID |
| bootstrap.nsg_name | Network Security Group Name |
| masters.nsg_id | Network Security Group ID |
| masters.nsg_name | nsg name |
| private_agents.nsg_id | Network Security Group ID |
| private_agents.nsg_name | nsg name |
| public_agents.nsg_id | Network Security Group ID |
| public_agents.nsg_name | nsg name |

