<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# VPC Peering

**Project Link:** [View Project](http://learn.nextwork.org/projects/aws-networks-peering)

**Author:** Shane Brown  
**Email:** shanebrown848@gmail.com

---

## VPC Peering

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_88727bef)

---

## Introducing Today's Project!

### What is Amazon VPC?

Amazon VPC is a service that lets you create your own isolated virtual network within the AWS Cloud. It allows you to define IP address ranges, create subnets, control routing, and apply security rules using security groups and network ACLs. Amazon VPC is useful because it gives you full control over how your AWS resources communicate, keeps traffic private and secure, and supports scalable architectures such as multi-VPC designs with features like VPC peering.

### How I used Amazon VPC in this project

In today’s project, I used Amazon VPC to create and manage two separate virtual networks with unique IP address ranges. I set up subnets, route tables, and security groups, then established a VPC peering connection between the two VPCs. I updated routing and security rules and used EC2 instances to test and verify private connectivity between the VPCs using ping.

### One thing I didn't expect in this project was...

One thing I didn’t expect in this project was how much manual configuration is required even after creating a VPC peering connection. I learned that peering alone doesn’t enable communication, and that route tables and security groups in both VPCs must be explicitly updated before traffic can flow between them.

### This project took me...

This project took me about an hour.

---

## In the first part of my project...

### Step 1 - Set up my VPC

In this step, I will create two separate Amazon VPCs using the VPC creation wizard. I am doing this to quickly set up multiple VPC environments and use the visual resource map to understand how each VPC’s networking components are created and connected. This prepares both VPCs for the peering connection in the next steps.

### Step 2 - Create a Peering Connection

In this step, I will create a VPC peering connection to link my two VPCs together. I am doing this to allow resources in each VPC to communicate privately using their private IP addresses and to understand how AWS enables secure network communication between separate VPC environments.

### Step 3 - Update Route Tables

In this step, I will update the route tables in both VPCs to direct traffic through the VPC peering connection because peering alone does not automatically enable routing. Adding these routes allows resources in VPC 1 and VPC 2 to find each other and communicate using their private IP addresses.

### Step 4 - Launch EC2 Instances

In this step, I will launch an EC2 instance in each VPC so I can test connectivity across the VPC peering connection. I am doing this to verify that resources in separate VPCs can communicate with each other once routing and peering are correctly configured.

---

## Multi-VPC Architecture

I started my project by launching two separate Amazon VPCs using the VPC creation wizard. Each VPC was created with one Availability Zone and one public subnet, and no private subnets. In total, I created two VPCs and two public subnets, one subnet in each VPC, to prepare them for setting up VPC peering in the next steps.

The CIDR blocks for VPCs 1 and 2 are 10.1.0.0/16 and 10.2.0.0/16. They have to be unique because each VPC must use a non-overlapping IP address range to avoid routing conflicts. If two VPCs shared the same CIDR block, AWS would not be able to correctly route traffic between resources, especially when setting up connections like VPC peering.

### I also launched 2 EC2 instances

I didn’t set up key pairs for these EC2 instances as I planned to use EC2 Instance Connect to access them instead. EC2 Instance Connect securely manages temporary SSH keys through the AWS Management Console, so I did not need to create or manage my own key pairs for this project.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_11111111)

---

## VPC Peering

A VPC peering connection is a networking link between two Amazon VPCs that allows resources in each VPC to communicate with each other using private IP addresses. It enables secure, low-latency traffic between VPCs without using the public internet and requires proper routing and security configurations to allow communication.

VPCs would use peering connections to allow secure, private communication between resources in different VPCs without sending traffic over the public internet. Peering connections make it possible to share services, connect environments like development and production, and build multi-VPC architectures while keeping network traffic isolated, low-latency, and secure.

The difference between a Requester and an Accepter in a peering connection is that the Requester is the VPC that initiates and sends the peering connection request, while the Accepter is the VPC that receives the request and must approve it. The peering connection only becomes active after the Accepter accepts the request, which ensures both VPC owners agree to the connection.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_1cbb1b88)

---

## Updating route tables

After accepting a peering connection, my VPCs’ route tables need to be updated because peering connections do not automatically route traffic between VPCs. Adding routes tells each VPC where to send traffic destined for the other VPC’s CIDR block and directs that traffic through the peering connection, allowing resources in both VPCs to communicate using private IP addresses.

My VPCs’ new routes have a destination of 10.2.0.0/16 in VPC 1 and 10.1.0.0/16 in VPC 2. The routes’ target was the VPC peering connection between VPC 1 and VPC 2, which directs traffic between the two VPCs using private IP addresses.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_4a9e8014)

---

## In the second part of my project...

### Step 5 - Use EC2 Instance Connect

In this step, I will use EC2 Instance Connect to connect to the EC2 instance in my first VPC so I can test communication across the VPC peering connection. I am doing this to verify that the instances can reach each other and to troubleshoot and fix any connectivity issues caused by routing or security configurations

### Step 6 - Connect to EC2 Instance 1

In this step, I will use EC2 Instance Connect again to connect to the EC2 instance in VPC 1 now that a public IP address has been assigned. I am doing this to confirm that the connectivity issue is resolved and to troubleshoot and fix any remaining configuration problems preventing access to the instance.

### Step 7 - Test VPC Peering

In this step, I will test connectivity between the EC2 instance in VPC 1 and the EC2 instance in VPC 2. I am doing this to verify that the VPC peering connection and route table updates are working correctly, and to troubleshoot and fix any security or networking issues until both instances can successfully communicate with each other.

---

## Troubleshooting Instance Connect

Next, I used EC2 Instance Connect to securely connect to my EC2 instance through the AWS Management Console without managing my own SSH key pairs. This allowed me to quickly access the instance to test connectivity and troubleshoot issues while AWS handled the temporary SSH credentials for me.

I was stopped from using EC2 Instance Connect as the EC2 instance did not have a public IPv4 address assigned to it. EC2 Instance Connect requires a public IP address to establish an SSH connection from the AWS Management Console, so the connection failed until I associated an Elastic IP address with the instance.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_7685490c)

---

## Elastic IP addresses

To resolve this error, I set up Elastic IP addresses. Elastic IP addresses are static, public IPv4 addresses provided by AWS that you can allocate to your account and associate with resources like EC2 instances. They allow an instance to have a consistent public IP address that does not change when the instance is stopped or restarted, making it reliable for remote access and connectivity.

Associating an Elastic IP address resolved the error because it provided the EC2 instance with a public IPv4 address. EC2 Instance Connect requires a public IP to establish an SSH connection from the AWS Management Console, and without one the instance was unreachable. Once the Elastic IP was attached, the instance became accessible and the connection succeeded.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_45663498)

---

## Troubleshooting ping issues

To test VPC peering, I ran the command ping 10.2.14.153 from the EC2 instance in VPC 1. This command sent ICMP requests across the VPC peering connection to verify that the two VPCs could communicate using private IP addresses.

A successful ping test would validate my VPC peering connection because it confirms that network traffic can travel between resources in different VPCs using private IP addresses. Receiving ping replies shows that the peering connection, route tables, and security group rules are correctly configured to allow ICMP traffic to pass between the two VPCs.

I had to update my second EC2 instance’s security group because inbound ICMP traffic from the first VPC was being blocked, which prevented the ping test from succeeding. I added a new inbound rule that allowed All ICMP – IPv4 traffic with the source set to the CIDR block of VPC 1 (10.1.0.0/16), enabling the two instances to communicate across the VPC peering connection.

![Image](http://learn.nextwork.org/encouraged_yellow_silly_yeti/uploads/aws-networks-peering_7a29d352)

---

---
