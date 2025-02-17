# AWS Launch Templates
This module used to create Launch Templates for Node groups or Karpenter.

## Usage
This example shows how to consume the `launch-templates` module. See this full [example](../../examples/karpenter/main.tf).

```hcl
module "launch_templates" {
  source                         = "aws-samples/aws-eks-accelerator-for-terraform//modules/launch-templates"
  tags                           = { Name = "terraform-ssp-eks"}
  eks_cluster_id                 = "<Enter EKS CLuster ID>"

  launch_template_config = {
    io1 = {
      ami                         = "ami-0adc757be1e4e11a1"
      launch_template_prefix      = "io1"
      launch_template_os          = "amazonlinux2eks"
      vpc_security_group_ids      = "<comma separated security groups ids>"
      iam_instance_profile        = "IAM Instance Profile"
      block_device_mappings       = [
        {
          device_name = "/dev/xvda"
          volume_type = "io1"
          volume_size = "200"
          iops = 100          # io1 and io2 -> Min: 100 IOPS, Max: 100000 IOPS (up to 1000 IOPS per GiB)
        }
      ]
    },
    io2 = {
      ami                          = "ami-0adc757be1e4e11a1"
      launch_template_prefix       = "io2"
      launch_template_os           = "amazonlinux2eks"
      vpc_security_group_ids       = "<comma separated security groups ids>"
      iam_instance_profile         = "IAM Instance Profile"
      block_device_mappings        = [
        {
          device_name = "/dev/xvda"
          volume_type = "io2"
          volume_size = "200"
          iops = 3000             #gp3-> Min: 3000 IOPS, Max: 16000 IOPS.
        }
      ]
    },
    gp3 = {
      ami                          = "ami-0adc757be1e4e11a1"
      launch_template_prefix       = "gp3"
      launch_template_os           = "amazonlinux2eks"
      vpc_security_group_ids       = "<comma separated security groups ids>"
      iam_instance_profile         = "IAM Instance Profile"
      block_device_mappings        = [
        {
          device_name = "/dev/xvda"
          volume_type = "gp3"
          volume_size = "200"
          iops = 3000             # gp3 -> Min: 3000 IOPS, Max: 16000 IOPS.
          throughput = 1000       # gp3 -> 125 to 1000
        }
      ]
    },
    gp2 = {
      ami = "ami-0adc757be1e4e11a1"
      ami                          = "ami-0adc757be1e4e11a1"
      launch_template_prefix       = "gp2"
      launch_template_os           = "amazonlinux2eks"
      vpc_security_group_ids       = "<comma separated security groups ids>"
      iam_instance_profile         = "IAM Instance Profile"
      block_device_mappings        = [
        {
          device_name = "/dev/xvda"
          volume_type = "gp2"
          volume_size = "200"
        }
      ]
    },
    bottlerocket = {
      ami                           = "ami-03909df9bfcc1e215"
      launch_template_os            = "bottlerocket"
      launch_template_prefix        = "bottle"
      vpc_security_group_ids        = "<comma separated security groups ids>"
      iam_instance_profile          = "IAM Instance Profile"
      block_device_mappings         = [
        {
          device_name = "/dev/xvda"
          volume_type = "gp2"
          volume_size = "200"
        }
      ]
    },
  }
}
```


<!--- BEGIN_TF_DOCS --->
## Requirements

No requirements.

## Providers

| Name | Version |
|------|---------|
| <a name="provider_aws"></a> [aws](#provider\_aws) | n/a |

## Modules

No modules.

## Resources

| Name | Type |
|------|------|
| [aws_launch_template.this](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/resources/launch_template) | resource |
| [aws_eks_cluster.eks](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_cluster) | data source |
| [aws_eks_cluster_auth.eks](https://registry.terraform.io/providers/hashicorp/aws/latest/docs/data-sources/eks_cluster_auth) | data source |

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|:--------:|
| <a name="input_eks_cluster_id"></a> [eks\_cluster\_id](#input\_eks\_cluster\_id) | EKS Cluster ID | `string` | n/a | yes |
| <a name="input_launch_template_config"></a> [launch\_template\_config](#input\_launch\_template\_config) | Launch template configuration | <pre>map(object({<br>    ami                    = string<br>    launch_template_os     = optional(string)<br>    launch_template_prefix = string<br>    iam_instance_profile   = optional(string)<br>    vpc_security_group_ids = optional(list(string)) # conflicts with network_interfaces<br><br>    network_interfaces = optional(list(object({<br>      public_ip       = optional(bool)<br>      security_groups = optional(list(string))<br>    })))<br><br>    block_device_mappings = list(object({<br>      device_name           = string<br>      volume_type           = string<br>      volume_size           = string<br>      delete_on_termination = optional(bool)<br>      encrypted             = optional(bool)<br>      kms_key_id            = optional(string)<br>      iops                  = optional(string)<br>      throughput            = optional(string)<br>    }))<br><br>    pre_userdata         = optional(string)<br>    bootstrap_extra_args = optional(string)<br>    post_userdata        = optional(string)<br>    kubelet_extra_args   = optional(string)<br><br>    http_endpoint               = optional(string)<br>    http_tokens                 = optional(string)<br>    http_put_response_hop_limit = optional(number)<br>  }))</pre> | n/a | yes |
| <a name="input_tags"></a> [tags](#input\_tags) | Additional tags (e.g. `map('BusinessUnit`,`XYZ`) | `map(string)` | `{}` | no |

## Outputs

| Name | Description |
|------|-------------|
| <a name="output_launch_template_arn"></a> [launch\_template\_arn](#output\_launch\_template\_arn) | Launch Template ARNs |
| <a name="output_launch_template_id"></a> [launch\_template\_id](#output\_launch\_template\_id) | Launch Template IDs |
| <a name="output_launch_template_image_id"></a> [launch\_template\_image\_id](#output\_launch\_template\_image\_id) | Launch Template Image IDs |
| <a name="output_launch_template_name"></a> [launch\_template\_name](#output\_launch\_template\_name) | Launch Template Names |

<!--- END_TF_DOCS --->
