# AWS CloudFormation Template to Install WordPress on an EC2 Instance

## Overview

This is a AWS Cloudformation template which automate the installation and configuration of WordPress in AWS, using Masterless Puppet.

Puppet module used in this template: https://forge.puppet.com/hunner/wordpress

AWS Cfn Template References:

https://s3-us-west-2.amazonaws.com/cloudformation-templates-us-west-2/VPC_With_PublicIPs_And_DNS.template

https://s3-us-west-2.amazonaws.com/cloudformation-templates-us-west-2/WordPress_Chef.template

## Capabilities

#### Installation includes:

- Create a VPC with a public subnet
- Create a AWS EC2 instance to host WordPress webserver and MySQL database
- Create a MySQL database as a respository database of WordPress on the same host


#### Requires:

- A valid AWS account (console or API)
- Proper IAM role to access resources like VPCs, Subnets, InternetGateway Security Groups, EC2 instances, CloudFomration etc.
- Amazon Linux is requred. The template could work on RHEL 6/7 and CentOS 6/7 with minor changes in 'UserData'

#### Puppet is used to automate the following tasks:
1) Create WordPress OS user and Group
2) Install apache
3) Install and create MySQL database as repository database for WordPress
4) Install and configure WordPress


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
