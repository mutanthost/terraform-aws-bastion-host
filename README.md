## About

Creates bastion host with allowed SSH access from specific IPs.

Features:
* Allow access from specific CIDRs (Default is `0.0.0.0/0`)

## Usage

Default
```
module "bastion" {
  source            = "github.com/jetbrains-infra/terraform-aws-bastion-host"  
  subnet_id         = "${aws_subnet.public.id}"
  internal_networks = ["10.0.10.0/24","${module.vpc.subnet_internal1_cidr_block}"]
}
``` 

All params
```
module "bastion" {
  source            = "github.com/jetbrains-infra/terraform-aws-bastion-host"  
  subnet_id         = "${aws_subnet.public.id}"
  allowed_hosts     = ["11.22.33.44/32","99.88.77.66./24"]
  internal_networks = ["10.0.10.0/24","${module.vpc.subnet_internal1_cidr_block}"]
  disk_size         = 10
  instance_type     = "t2.micro"
}
```

## Params

* `subnet_id` - The VPC Subnet ID to launch in.
* `allowed_hosts` - CIDR blocks of trusted networks.
* `internal_networks` - Internal network CIDR blocks.


### Optional params with default values

* `disk_size` - The size of the root volume in gigabytes (Default `10`).
* `instance_type` - The type of instance to start (Default `t2.micro`).

## Outputs

* `public_ip` - bastion public IP
* `internal_ip` - bastion internal IP
* `instance_id` - EC2 instance ID