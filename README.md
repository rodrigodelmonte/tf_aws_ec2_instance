ec2_instance terraform module
=======================

A terraform module for making ec2 instances.
* Assumes you're making your instances in a VPC.
* Does not do any block device configuration (yet)

Module Input Variables
----------------------

- `ami_id` - The AMI to use
- `number_of_instances`  - The number of instances you want made
- `subnet_id - The VPC subnet to place the instance in
- `instance_type` - The EC2 instance type, e.g. m1.small
- `instance_name` - The instance name you want, this is used to populate
    the Name tag.
- `user_data` - The path to the user_data file. Terraform will include the contents of this file while launching the instance
- `security_groups` - The security group ID.
- `tags` - A map for setting AWS tags.

Usage
-----

You can use this in your terraform template with the following steps.

1. Adding a module resource to your template, e.g. `main.tf`

```
module "ec2_instance" {
  source = "github.com/solarce/tf_aws_ec2_instance"
  instance_type = "${var.instance_type}"
  instance_name = "${var.instance_name}"
  ami_id = "${var.ami_id}"
  aws_access_key = "${var.aws_access_key}"
  aws_secret_key = "${var.aws_secret_key}"
  aws_region = "${var.aws_region}"
  subnet_id = "${var.subnet_id}"
  number_of_instances = "${var.number_of_instances}"
  security_groups = "{var.security_groups}"
  user_data = "{var.user_data}"
}
```

2. Setting values for the following variables, either through `terraform.tfvars` or `-var` arguments on the CLI

- aws_access_key
- aws_secret_key
- aws_region
- instance_name
- instance_type
- subnet_id
- ami_id
- security_groups
- number_of_instances

Authors
=======
This repository was forked from [terraform-community-modules](https://github.com/terraform-community-modules/tf_aws_ec2_instance)
Created and maintained by [Brandon Burton](https://github.com/solarce)
(brandon@inatree.org).

License
=======

Apache 2 Licensed. See LICENSE for full details.
