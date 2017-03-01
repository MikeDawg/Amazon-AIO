AMAZON-AIO (All in one)
=========
WORK IN PROGRESS!

A Training playbook to help get you started in AWS with Ansible.  This playbook in its current state (w/ a populated vars file) will deploy the following:

	VPC
	Network(s)
	Gateway(s)
	Routing
	Security Group(s)
	Load Balancer(s)
	Launch configuration(s)
	Auto Scaling Group(s)


Requirements
============

You will need an AWS account
You will need Acces Keys
You will need the following packages installed on the box you plan to run this playbook from:

	python
	python-dnf
	python-pip
	python-boto
	paramiko
	PyYAML
	jinja2
	httplib2
	libselinx-python.


Variables
=========

Variables are set to be called from the var/main.yml file.  The following var's are being called.  Please change as you see fit.

	key_name:
	vpc_name:
	cidr_block:
	instance_type:
	ami_image:
	aws_region:
	availability_zones:
	gateway_2a:
	gateway_2b:
	gateway_2c:
	ssh_lc_name:
	http_lc_name:

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
Sets up a single VPC in US-West-2 Region and an Internet-Gateway.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t vpc -k

Network:
========
Sets up six networks. Three tagged for public and three tagged for private.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t network -k

Gateways:
=========
Sets up Elastic IP's and NAT Gateways.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t gateways -k

Routing-Public:
===============
Sets up a routing table for the public subnets with the VPC's Internet Gateway.

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-public -k

Routing-Private:
================
Sets up routing tables for each of the private subnets.
(Still a work in progress.  Will need to manually add nat-gateway id's to vars file)

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
