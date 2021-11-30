Description of Resources Created

VPC
VPC is defined with CidrBlock 10.0.0.0/16.
DnsHostnames is set to 'true' to get public DNS hostname.

Subnet
Subnets : a private and a public subnet is defined in each Availability Zone.
Public Subnet 1 - in Availability Zone 1 with CidrBlock 10.0.1.0/24.
Public Subnet 2 - in Availability Zone 2 with CidrBlock 10.0.3.0/24.
Private Subnet 1 - in Availability Zone 1 with CidrBlock 10.0.2.0/24.
Private Subnet 2 - in Availability Zone 2 with CidrBlock 10.0.4.0/24.
 

Internet Gateway  
It provides a target for internet-routable traffic in your route tables.
Route tables refer Internet Gateway as target for Destination.
 

Route Tables 
1. Public Subnet
    Public Route Table : routes traffic either to Internet Gateway for outbounds or within 10.0.0.0/16.
    Public subnets in two Availability  Zones are associated  with the public route table.
2. Private Subnet
    Private Route Table : routes traffic only within 10.0.0.0/16.
    Private subnets are associated  with private route table.

EC2 Instances
Two EC2 Instances are defined in public subnet with user data to install Apache web server.
The Instances have a reference to  EC2 Security  group and KeyPair.
 
Security Groups: 
EC2 Security Group : Port 22 for SSH and Port 80 open to the Load Balancer.
ELB Security Group :  Port 80 open to everyone.

Application  Load Balancer : Load balancer is defined with Listener, target group and references ELB security group.
Listener : The Listener is set with port 80 and protocol HTTP. The Listener forwards the traffic  to targets in target group.

Target Group : One target group is defined with two EC2 Instances as targets. Health Check port is set to 80.