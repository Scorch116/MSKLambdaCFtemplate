# MSKLambdaCFtemplate

This template sets up a networking infrastructure with a VPC, subnets, routing, security groups, NAT gateways, and an MSK cluster.

It also provisions an EC2 instance (Client machine) and a Lambda function for interacting with the MSK cluster.

NOTE - Can take some time to provision, once it starts deploying in Cloud formation, get a coffee etc.

Summary of template resources

VPC, Subnets, and Routing tables and route associations
NAT gateways and elastic IPs are created to allow private subnets to access the internet while maintaining security.
A security group is created with inbound rules allowing access on ports 22, 443, 80, 9094, and 9092. It is associated with the MSK cluster and Lambda function.
IAM roles are created for the MSK cluster and EC2 instances
EC2 instance is launched in a public subnet, associated with the security group, and provided with user data to install Java and Kafka.
An MSK cluster is created with a specified Kafka version, broker node configurations, security groups, and client subnets. It also enables encryption in transit with plaintext.
A Lambda function is defined with a Python 3.9 runtime. It decodes and prints messages from Kafka records received as input.
This template sets up a networking infrastructure with a VPC, subnets, routing, security groups, NAT gateways, and an MSK cluster.
It also provisions an EC2 instance (Client machine) and a Lambda function for interacting with the MSK cluster.
Things to Note

I recommend deploying this template in a region you have little or no resources as it is resource heavy with NAT gateways and ENIs, the template default is US-EAST-1.
The Ec2 machine uses an AMi from AMI catalog, AMIs are a regional resource - default region will be us-east-1, if you are changing region, update the template to a AMI image in the region you wish to deploy.
