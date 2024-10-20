# Amazon Web Services

## Basic Networking Setup:

### VPC - Virtual Private Cloud [lies inside AWS Cloud]
- An isolated segment in AWS cloud, where we can put our own servers that are isolated and prevents anykind of access unless we configure it to provide some access.
- When we create a AWS cloud, it provides a default VPC with default configurations suitable for deployment, but it also makes things confusing.
- Create a new VPC from scratch, select VPC only option.
- Keep IPv4 CIDR : 10.0.0.0/16 and select No IPv6 CIDR block, Tenancy Default.
- VPC Created !!
- 10.0.0.0 --> CIDR block IP range, this is the range where we place our services, each service has an IP address that we'll need.
- The subnets will provide a range of those IP addresses where we can place our servers.
- VPC contains two types of Subnets.
### Public Subnet: 
- Accessible from anywhere
### Private Subnet:
- It should be accessible only within the VPC or maybe other subnets in the same VPC.

### Creating a Subnet:
- Add VPC ID associated with the IPv4 CIDR range 10.0.0.0/16
- name subnet: public-subnet
- select availability zone south-1a, if south-1a goes down south-1b is there for backup.
- IPv4 VPC CIDR block : 10.0.0.0/16
- IPv4 subnet CIDR block : 10.0.1.0/24
- range of IP addresses, a public subnet can hold : 0 to 256
- Each subnet is using addresses within AWS cloud

- Create a private subnet with zone south-1b and IPv4 subnet CIDR block = 10.0.2.0/24 and IPv4 VPC CIDR = 10.0.0.0/16

### VPC Internet Gateway:
- We need an Internet Gateway for a user client to access our VPC.
- We need to create a VPC Internet Gateway and that will provide a way to access our public subnet.
- Create an internet gateway
- Attach VPC you created to the internet gateway.
- Now, our VPC is connected to the internet.

### Route Tables
- Route table is something we need to attach to each public subnet and private subnet.
- These route tables provide where and what access is provided.
- Route tables require us to have the access to VPC internet gateway and the private route table should have access to public route table so the different subnet can communicate with each other.
- Basically Route tables provide a way to determine what routes can connect to which routes in the VPC.
- By default, VPCs have a route table attached to them.
- VPC basically has a main route table that allows local access to anything in the VPC.
- Create a seperate route table for each subnet so that each one has their own private access.
- Create public and private route tables attached to the VPC we created.
- Connect public route table with public subnet through Edit Subnet Associations.
- Connect private route table with private subnet through Edit Subnet Associations.

- Go to public route table and go to edit routes, add another route and add 0.0.0.0/0 and associate this route with VPC internet gateway.
- This represents every IP address out there, local as well as outside of the AWS including entire internet.
- This gives public route table access to the internet gateway and wider internet including outside the AWS cloud.
- Do not do the same with private route table, let it remain with private access connected to local route only.

### VPC Network Access Control List:
- Associated with each subnet, they are basically like firewalls for each subnet.
- We can use this to blacklist certain IP addresses to prevent things from coming in.

This was our Basic NETWORKING SETUP


## Amazon EC2 Instance [Hosting Backend]
- EC2 is basically like a server that we can just host anything we want.
- For our inventory managment system, we are hosting the backend on EC2 instance.
- Create an EC2 instance and name it ec2-inventorymanagement-backend, and choose Amazon Linux for quick start.
- keep instance type : t2.micro as it is free tier eligible.
- create a keypair name - standard-keypair
- In network settings, allow SSH traffic from anywhere (0.0.0.0/0)
- Allow HTTPS traffic from internet.
- Allow HTTP traffic from internet.
- Associate Public subnet.
- Enable Auto assign public IP

### Security Groups
- security group is a set of firewall rules that control traffic for your instance
- We have different security groups attached with different services like EC2 and RDS
- These security groups are like individual firewalls attached to specific services.
- Add 3 security group rules 1,2,3 as SSH, HTTPS and HTTP respectively with source type Anywhere.

Launch the EC2 Instance !!
Connect the EC2 Instance to check the status !!

# Inventory Management System - NextJS

[DataBase Modelling diagram](https://drawsql.app/teams/sai-sathwik/diagrams/inventorymanagement-data)

![image](https://github.com/user-attachments/assets/bf13cb24-ceb3-408f-8d8b-de53d4f7a63a)
