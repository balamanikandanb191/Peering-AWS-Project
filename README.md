# AWS VPC Peering Project

## Project Overview

This project demonstrates how to establish private network connectivity between two Amazon Virtual Private Clouds (VPCs) using **AWS VPC Peering**. The implementation includes EC2 instances, route table configuration, security group rules, and connectivity testing using private IP addresses.

## Architecture

The architecture consists of two VPCs in the AWS US East (N. Virginia) region.

| Component | VPC 1 | VPC 2 |
|---|---|---|
| VPC Name | `vpc1-vpc` | `vpc2-vpc` |
| IPv4 CIDR | `10.1.0.0/16` | `10.7.0.0/16` |
| Public Subnet | Yes | No |
| Private Subnet | Yes | Yes |
| EC2 Instances | Public and private EC2 | Private EC2 |
| Connectivity | VPC Peering | VPC Peering |

**AWS Region:** `us-east-1` (N. Virginia)

## Project Objectives

- Create and configure two VPCs with non-overlapping CIDR ranges.
- Deploy EC2 instances in public and private subnets.
- Establish a VPC Peering connection between the two VPCs.
- Configure route tables to enable private communication.
- Configure security group rules to allow required network traffic.
- Validate connectivity using ICMP ping between private IP addresses.

## Services Used

- Amazon VPC
- Amazon EC2
- VPC Peering
- Route Tables
- Internet Gateway
- Security Groups
- Linux Networking Utilities

## Implementation Steps

### 1. Create VPCs

Created two VPCs with separate IPv4 CIDR ranges:

- VPC 1: `10.1.0.0/16`
- VPC 2: `10.7.0.0/16`

The CIDR ranges do not overlap, allowing VPC Peering.

### 2. Create Subnets and EC2 Instances

Configured a public subnet and a private subnet in VPC 1, along with a private subnet in VPC 2.

Deployed three EC2 instances:

- `vm1vpc1` — VPC 1 public instance
- `vm2vpc1` — VPC 1 private instance
- `vm1vpc2` — VPC 2 private instance

### 3. Establish VPC Peering

Created and accepted a VPC Peering connection between VPC 1 and VPC 2.

**Peering Connection Status:** Active

### 4. Configure Route Tables

Added routes to enable traffic between the VPCs.

**VPC 1 private route table**

| Destination | Target |
|---|---|
| `10.7.0.0/16` | VPC Peering connection |

**VPC 2 private route table**

| Destination | Target |
|---|---|
| `10.1.0.0/16` | VPC Peering connection |

The routes were saved successfully and displayed an Active status.

### 5. Configure Security Groups

Configured security group rules to permit the required traffic between EC2 instances in the two VPCs. ICMP traffic was allowed for connectivity testing.

### 6. Test Connectivity

Used the Linux `ping` command to test connectivity between private IP addresses across the VPC Peering connection.

Example:

```bash
ping -c 4 <destination-private-ip>
```

**Observed Result:** ICMP echo replies were received from private IP address `10.1.134.157`, confirming successful connectivity to that destination across the configured network path.

## Project Outcome

- Successfully established an Active VPC Peering connection.
- Configured routes in both VPCs.
- Verified private IP connectivity using ICMP.
- Demonstrated private communication between resources across two VPCs.

## Key Learnings

- VPC CIDR ranges must not overlap for VPC Peering.
- Routes must be configured in both directions.
- Security groups and network ACLs must permit the required traffic.
- VPC Peering does not automatically provide internet access to private instances.
- VPC Peering is not transitive; traffic cannot automatically pass through one peering connection to reach another VPC.

## Project Evidence

Add your screenshots to this repository to document the implementation:

1. VPC configuration and CIDR ranges
2. EC2 instances and subnet placement
3. Active VPC Peering connection
4. VPC 1 route table
5. VPC 2 route table
6. Successful private IP ping test

## Author

**Balamanikandan S.**

Cloud Infrastructure | AWS | Microsoft Azure

---

*This project was completed as a hands-on AWS networking lab to understand VPC Peering and private network connectivity.*
