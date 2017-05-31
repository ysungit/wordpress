# AWS CloudFormation Template to Install WordPress on(AWS) EC2 Instance

## Overview

This is a AWS Cloudformation template which automate installation and configuration of WordPress in AWS, using Masterless Puppet.

Puppet module used in this template: https://forge.puppet.com/hunner/wordpress

## Capabilities

#### Installation includes:

- Create a VPC with a public subnet
- Create a AWS EC2 instance to host WordPress webserver and MySQL database
- Create a MySQL database as a respository database of WordPress on the same host


#### Requires:

- A valid AWS account (console or API)
- Proper IAM role to access resources like VPCs, Subnets, InternetGateway Security Groups, EC2 instances, CloudFomration etc.


## Parameters
- `DBPassword`: MySQL 'wordpress' password
- `DBRootPassword`: MySQL 'root' password
- `EC2InstanceType`: Webserver instance type; default 't2.small'
- `KeyName`: pick one from the list of existing keypair
- `SSHLocation`: SSH (port 80) IP range; default to 0.0.0.0/0

## Outputs
- `VPCId`: VPCId of the newly created VPC
- `PublicSubnet`: SubnetId of the public subnet
- `DNSName`: DNS Name of the EC2 host
- `WebsiteURL`: WordPress Website URL
