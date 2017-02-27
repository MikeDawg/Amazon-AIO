AMAZON-AIO (All in one)
=========

A simple playbook to help get you started in AWS with Ansible.  This playbook in its current state (w/ a populated vars file) will deploy the following:

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


Playbook Examples
=================

VPC:
====
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t vpc -k

Network:
========
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t network -k

Gateways:
=========
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t gateways -k

Routing-Public:
===============
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-public -k

Routing-Private:
================
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-private-2a -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-private-2b -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t routing-private-2c -k

Security Groups:
================
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t sec-grp-ssh -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t sec-grp-http -k

Elastic Load Balancers:
=======================
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t elb-public -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t elb-private -k

Launch configuration:
=====================
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t vpc-lc-ssh -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t vpc-lc-http -k

Auto Scaling Group:
===================
ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t asg-ssh -k

ansible-playbook -i inventory/local.yml Amazon-Setup.yml -t asg-http -k

License
=======

BSD

Author Information
==================

Adam A. Valenzuela - Brevity is the Soul of Wit
# Ansible
