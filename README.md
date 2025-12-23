# VPC Peering

**Project Link:** https://learn.nextwork.org/projects/aws-networks-peering  
**Author:** Shane Brown  

---

## Overview

This project focuses on connecting multiple Amazon Virtual Private Clouds (VPCs) using VPC peering. The goal is to understand how separate cloud networks communicate privately and how routing and security configurations enable or block traffic between them.

This project demonstrates how multi-VPC architectures are designed and managed in real-world AWS environments. :contentReference[oaicite:0]{index=0}

---

## What I built

I created two separate Amazon VPCs and connected them using a VPC peering connection. This included:

- Creating two VPCs with unique, non-overlapping CIDR blocks  
- Establishing a VPC peering connection between the VPCs  
- Updating route tables in both VPCs to enable traffic flow  
- Launching EC2 instances in each VPC  
- Testing private connectivity between VPCs using ICMP  

This setup mirrors common production architectures where services are segmented across multiple VPCs while remaining privately connected. :contentReference[oaicite:1]{index=1}

---

## Key concepts learned

- What VPC peering is and when it’s used  
- Why VPCs must have unique CIDR blocks  
- The difference between requester and accepter VPCs  
- How route tables enable communication across peered VPCs  
- How security groups affect cross-VPC traffic  
- How Elastic IPs and EC2 Instance Connect support access and testing :contentReference[oaicite:2]{index=2}

---

## How VPC peering works

A VPC peering connection allows two VPCs to communicate using private IP addresses without sending traffic over the public internet. Once a peering connection is established and accepted, routing and security rules must be configured on both sides to allow traffic.

Peering connections are commonly used to connect environments such as development, staging, and production, or to share services across isolated networks. :contentReference[oaicite:3]{index=3}

---

## Testing and troubleshooting

I tested connectivity between EC2 instances in each VPC using the `ping` command. When connectivity failed, I troubleshot the issue by checking:

- Route table entries in both VPCs  
- Security group inbound and outbound rules  
- Instance accessibility using EC2 Instance Connect  

Updating the security groups to allow ICMP traffic between the VPC CIDR ranges resolved the issue and confirmed successful peering. :contentReference[oaicite:4]{index=4}

---

## Why this project matters

Multi-VPC architectures are common in AWS for scalability, security, and organizational separation. Understanding how to securely connect VPCs while maintaining isolation is a critical skill for cloud engineers and security professionals.

This project demonstrates how private cloud networks communicate and how misconfigurations are identified and resolved. :contentReference[oaicite:5]{index=5}

---

## Documentation

📄 **Full project documentation:**  
[documentation.md](./documentation.md)

This file includes step-by-step configuration details, testing commands, troubleshooting notes, and reflections from completing the project.

---

## Credits

Built as part of the **NextWork** AWS networking learning series.
