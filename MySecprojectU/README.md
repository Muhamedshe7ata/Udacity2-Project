# Udagram-Project for Udacity Cloud DevOps Nanodegree project 02
Deploying high-availability web app using AWS CloudFormation

## Description
Using AWS CloudFormation, created a script to deploy a highly available web app

## Work Flow
- Build a diagram to visualize main parts of the infrastructure and for better understanding the script. 
- Create network infrastructure components stack in a "YAML" formatted template.
- Create servers stack, security roles and software in a separate template.
- Using paramteters and outputs to make cloudformation templates more reusable (In both templates).

## Specifications
- Servers are distributed in multiple Availability Zones to make the app highly available.
- Created LaunchConfiguration for application servers to have at least four servers, two located in each AZ. 
- The launch configuration will be used by an Auto-Scaling Group.
- Each server will have two vCPUs, at least 4GB of RAM and at least 10GB volume size. The used Operating System is Ubuntu 18.
- Used a userdata script to install Apache2 server at instance launch.

## Security
- Servers will have ***Read Only*** access to S3 service. (In case needed to download any further app data).
- All  inbound traffic will be allowed only from **Port 80** in all resources (Security groups, health checks and listeners associated with the load balancer)
- Servers are located in private subnets so thery're not accessible from outside internet.
- Website is only accessible through the load balancer which is located in a public subnet.
- A Bastion host located in a public subnet is used to SSH web servers for maintainance purpose and it's accessible through SSH from ***My local IP address only***

#
-Create stack for Network:
aws cloudformation create-stack --stack-name network --template-body file://Network.yml --parameters file://Network-parameters.json


-Create stack for Servers:

aws cloudformation create-stack --stack-name server --template-body file://Servers.yml --parameters file://Servers-parameters.json --capabilities "CAPABILITY_IAM" "CAPABILITY_NAMED_IAM"

#
## -You can check :
http://serve-WebAp-INA3P9BHOHBS-158820225.us-east-1.elb.amazonaws.com

## For Diagram created :
 https://lucid.app/documents/view/85d744be-1a33-40e9-9664-114f8f0b7813





