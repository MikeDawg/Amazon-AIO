AMAZON-AIO (All in one)
=========


This is a Training playbook to help get you started in AWS with Ansible.  These roles are designed to be run one at a time to see the progression of whats developing in AWS.  This playbook in its current state (w/ a populated vars file) will deploy the following:

	VPC
	Network(s)
	Gateway(s)
	Routing Table(s)
	Security Group(s)
	Load Balancer(s)
	Launch configuration(s)
	Auto Scaling Group(s)


Requirements
============

You will need an AWS account; You will need AWS Access and secret Keys exported or setup via boto.
The "pre-flight" role will help you install the needed packages on the box you plan to run this playbook from:

YUM
  epel-release
	python-pip
	libselinx-python

PIP
  awscli
	saws
	boto
	botocore
	boto3

Variables
=========

Variables are set to be called from the var/main.yml file.  The following var's will need to be set as they are called multiple times.
Please change as you see fit.

	key_name:
	vpc_name:
	cidr_block:
	instance_type:
	ami_image:
	aws_region:
	aws_dns_support:
	availability_zones:
	gateway_2a:
	gateway_2b:
	gateway_2c:
	ssh_lc_name:
	http_lc_name:
	aws_lc_config_ssh:
	aws_lc_config_http:

Dependencies
============

To get started with dynamic inventory management, you’ll need to grab the EC2.py script and the EC2.ini config file. The EC2.py script is written using the Boto EC2 library and will query AWS for your running Amazon EC2 instances. The EC2.ini file is the config file for EC2.py, and can be used to limit the scope of Ansible’s reach. You can specify the regions, instance tags, or roles that the EC2.py script will find.  
	https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.py
	https://raw.githubusercontent.com/ansible/ansible/devel/contrib/inventory/ec2.ini

Or have a quick look at
	https://aws.amazon.com/blogs/apn/getting-started-with-ansible-and-dynamic-amazon-ec2-inventory-management/


Playbook Roles
=================

Pre-Flight:
============
Sets up your host to play with AWS.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t pre-flight -k

VPC:
====
Sets up a single VPC in US-West-2 Region.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t vpc -k

Network:
========
Sets up six subnets. Three tagged for public and three tagged for private.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t network -k

Gateways:
=========
Sets up an Internet Gateway, 3x Elastic IP's for NAT Gateways.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t gateways -k

Routing-Public:
===============
Sets up a routing table for the public subnets with the VPC's Internet Gateway.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-public -k

Routing-Private:
================
Sets up routing tables for each of the private subnets.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-private-2a -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-private-2b -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-private-2c -k

Security Groups:
================
Sets up Basic security groups.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t sec-ssh -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t sec-http -k

Load Balancers:
================
Sets up one Internet-Facing load balancer and one Internal load balancer.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t elb-public -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t elb-private -k

Launch configuration:
=====================
Sets up two basic Launch configurations.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t lc-ssh -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t lc-http -k

Auto Scaling Group:
===================
Sets up two Auto-scaling groups based on the Launch configurations.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t asg-ssh -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t asg-http -k

License
=======

MIT

Author Information
==================

Adam A. Valenzuela - Brevity is the Soul of Wit.
# Ansible
