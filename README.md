# Creating_AWS_EC2_Instances_Using_Terraform_part-1
- create a folder in the local machine
- open that folder with VSCode
- create file main.tf
- install terraform then in the terminal write terraform -v
  
# Create an IAM user in AWS then attach administrator policy then create a secret key, secret access key 
- find out ami from your AWS EC2 ami ID

# main.tf 
- ignore the left indentations below. (see the link https://registry.terraform.io/providers/hashicorp/aws/latest/docs )
- 
-terraform {
-  required_providers {
-    aws = {
-      source  = "hashicorp/aws"
-     version = "~> 4.0"
-    }
-  }
-}

-provider "aws"{
-    region = "us-east-1"
-    access_key = "AK132323235656565623233"
-    secret_key = "NTe1212dsf2121215521212122sf1fsfsf"
-}

-resource "tls_private_key" "rsa_4096" {
-  algorithm   = "RSA"
-  rsa_bits = 4096
-}

-variable "key_name" {}

-resource "aws_key_pair" "key_pair" {
-  key_name   = var.key_name
-  public_key = tls_private_key.rsa_4096.public_key_openssh
-}

-resource "local_file" "private_key" {
-  content = tls_private_key.rsa_4096.private_key_pem
-  filename =var.key_name
-}

-resource "aws_instance" "public_instance" {
-  ami           = "ami-056654654656rnjhsh"
-  instance_type = "t2.micro"
-  key_name = aws_key_pair.key_pair.key_name
-
-  tags = {
-    Name = "public_instance"
-  }
-}


# Next Steps: Terraform commands 
- terraform init
- terraform plan 
- terraform apply
# EC2 Instance Created !! Check your AWS console
- after finishing the lab, don't forget to destroy the running ec2 instances
- pass command: terraform destroy
# No running EC2 instance existed now!
- Please consider sharing it with your peers/team. Thank YOU

