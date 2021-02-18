# vpc_project
team2


Types of resources are supported:
VPC
Subnet
Internet Gateway
Nat Gateway
Route 53

Terraform versions: 0.14
For creating VPC

* resource “aws_vpc” “main” {
 2.  cidr_block = “${var.cidr_block}”
 3. tags       = “${var.tags}”
 4.  }

For creating subnet
resource "aws_subnet" "main" {
  vpc_id     = aws_vpc.main.id
  cidr_block = "10.0.1.0/24"
