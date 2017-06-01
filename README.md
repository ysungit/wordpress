# AWS CloudFormation Template to Install WordPress on an EC2 Instance

## Overview

This is a AWS CloudFormation template which automates the installation and configuration of WordPress in AWS, using Masterless Puppet.

Puppet WordPress module is used in this template: https://forge.puppet.com/hunner/wordpress

Sample AWS CloudFormation Templates:

https://s3-us-west-2.amazonaws.com/cloudformation-templates-us-west-2/VPC_With_PublicIPs_And_DNS.template

https://s3-us-west-2.amazonaws.com/cloudformation-templates-us-west-2/WordPress_Chef.template

## Capabilities

#### Installation includes:

- Create a VPC with a public subnet
- Create a AWS EC2 instance to host WordPress web server and MySQL database
- Create a MySQL database as a repository database of WordPress on the web server host
- Install and configure WordPress web server


#### Requires:

- A valid AWS account (console or API)
- Proper AWS IAM role to access AWS resources: VPCs, Subnets, Internet Gateway, Security Groups, EC2 instances, CloudFormation etc.
- Amazon Linux is required. The template would work on RHEL 6/7 and CentOS 6/7 with some changes in 'UserData' (eg. additional steps to install aws-cfn-bootstrap)

#### The CloudFormation template creates the following AWS resources:
- A VPC and a subnet
- Network ACLs
- An Internet Gateway and a Routing table
- An EC2 instance as WordPress web server and MySQL database server
- A Web server Security Group

#### Puppet is used to automate the following tasks:
1) Create WordPress OS user and Group
2) Install and configure Apache (**puppetlabs-apache** https://forge.puppet.com/puppetlabs/apache)
3) Install, create and configure MySQL database (**puppetlabs-mysql** https://forge.puppet.com/puppetlabs/mysql)
4) Install and configure WordPress (**hunner-wordpress** https://forge.puppet.com/hunner/wordpress)

#### Assumptions:

- No Puppet master is required; standalone/masterless Puppet is used in this template
- No external/existing database is available for WordPress; a new MySQL database is created on the web server host
- No Disaster Recovery or High Availability is required (single EC2 instance running on a single AZ)
- No scaling requirement (no AWS ELB and ASG etc)


## CloudFormation Parameters
- `DBPassword`: MySQL 'wordpress' password
- `DBRootPassword`: MySQL 'root' password
- `EC2InstanceType`: Webserver instance type; default 't2.small'
- `KeyName`: dropdown list of existing keypairs
- `SSHLocation`: SSH (port 80) IP range; default to 0.0.0.0/0

## CloudFormation Outputs
- `VPCId`: VPCId of the newly created VPC
- `PublicSubnet`: SubnetId of the public subnet
- `DNSName`: DNS Name of the EC2 host
- `WebsiteURL`: WordPress Website URL
