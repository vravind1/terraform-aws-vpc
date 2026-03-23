# terraform-aws-vpc

Private registry module that provisions a production-ready AWS VPC with public and private subnets, an Internet Gateway, and route tables.

## Usage

```hcl
module "vpc" {
  source  = "app.terraform.io/vishnu-test-org/vpc/aws"
  version = "1.0.0"

  name        = "my-app"
  environment = "production"
  cidr_block  = "10.0.0.0/16"

  availability_zones   = ["us-east-1a", "us-east-1b"]
  public_subnet_cidrs  = ["10.0.1.0/24", "10.0.2.0/24"]
  private_subnet_cidrs = ["10.0.101.0/24", "10.0.102.0/24"]
}
```

## Resources Created

- `aws_vpc`
- `aws_internet_gateway`
- `aws_subnet` (public × N)
- `aws_subnet` (private × N)
- `aws_route_table` (public)
- `aws_route_table_association`

## Inputs

| Name | Description | Type | Default | Required |
|------|-------------|------|---------|----------|
| name | Name prefix for all resources | string | — | yes |
| cidr_block | VPC CIDR block | string | 10.0.0.0/16 | no |
| environment | Environment name | string | — | yes |
| availability_zones | AZs for subnets | list(string) | us-east-1a/b | no |
| public_subnet_cidrs | CIDRs for public subnets | list(string) | — | no |
| private_subnet_cidrs | CIDRs for private subnets | list(string) | — | no |
| tags | Additional tags | map(string) | {} | no |

## Outputs

| Name | Description |
|------|-------------|
| vpc_id | VPC ID |
| vpc_cidr_block | VPC CIDR block |
| public_subnet_ids | List of public subnet IDs |
| private_subnet_ids | List of private subnet IDs |
| internet_gateway_id | Internet Gateway ID |
