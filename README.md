# vpc_project
team2
AWS_Terraform VPC module

Terraform: Use Infrastructure as Code to provision and manage any cloud, infrastucture, or service.

Types of resources are supported:
VPC
Subnet
Internet Gateway
Nat Gateway
        Terraform versions: latest 0.14
  Provider.tf Configure the AWS provider
  
  provider "aws" {
  region = "${var.region}"
}
  Provisioner.tf Provisioners can be used to model specific actions on the local machine or on a remote machine in order to prepare servers or other infrastructure objects for service.
     
For creating VPC: vpc.tf
This resource can prove useful when a module accepts a vpc id as an input variable and needs to, for example, determine the CIDR block of that VPC.

resource "aws_vpc" "main" {
  cidr_block = "${var.cidr_block}"
  tags       = "${var.tags}"
}

For creating SG  security.tf
resource "aws_security_group" "vpc_task" {
  name        = "vpc_task"
  description = "Allow TLS inbound traffic"

  ingress {
    description = "Allow ssh"
    from_port   = 22
    to_port     = 22
    protocol    = "tcp"
    cidr_blocks = ["0.0.0.0/0"]
  }

  egress {
    from_port   = 0
    to_port     = 0
    protocol    = "-1"
    cidr_blocks = ["0.0.0.0/0"]
  }

  tags = "${var.tags}"
  
  Private and public subnets
aws_subnet provides details about a specific VPC subnet.
resource "aws_subnet" "subnet1" {
  vpc_id     = "${aws_vpc.main.id}"
  cidr_block = "${var.private_cidr_block1}"
  tags       = "${var.tags}"
}

resource "aws_subnet" "subnet2" {
  vpc_id     = "${aws_vpc.main.id}"
  cidr_block = "${var.private_cidr_block2}"
  tags       = "${var.tags}"
}

resource "aws_subnet" "subnet3" {
  vpc_id     = "${aws_vpc.main.id}"
  cidr_block = "${var.private_cidr_block3}"
  tags       = "${var.tags}"
}

resource "aws_subnet" "subnet101" {
  vpc_id                  = "${aws_vpc.main.id}"
  map_public_ip_on_launch = true
  cidr_block              = "${var.public_cidr_block1}"
  tags                    = "${var.tags}"
}

resource "aws_subnet" "subnet102" {
  vpc_id                  = "${aws_vpc.main.id}"
  map_public_ip_on_launch = true
  cidr_block              = "${var.public_cidr_block2}"
  tags                    = "${var.tags}"
}

resource "aws_subnet" "subnet103" {
  vpc_id                  = "${aws_vpc.main.id}"
  map_public_ip_on_launch = true
  cidr_block              = "${var.public_cidr_block3}"
  tags                    = "${var.tags}"
