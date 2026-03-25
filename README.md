
# Secure Cloud Environment with Attack Detection (Azure)

## Overview
This project demonstrates the design, deployment, and security hardening of a cloud environment in Microsoft Azure, including attack detection and monitoring capabilities. 

The environment was built under Azure subscription constraints, requiring adaptation to policy-enforced region restrictions and resource limitations. These constraints reflect real-world cloud scenarios where engineers must design secure systems within operational boundaries.

The project focuses on identifying misconfigurations, applying security controls, implementing logging and alerting, and simulating attack scenarios to validate detection and response mechanisms.

## Objectives
- Deploy a cloud-based VM
- Identify security misconfiguration
- Apply security hardening techniques
- Implement logging and monitoring
- Simulate and detect attacks.

## Day 1 Setup
- Created Resource Group
<img width="1918" height="856" alt="1 1  Resource Group" src="https://github.com/user-attachments/assets/a0fbba0e-c3c7-4067-b5a2-d4e5f53522fe" />

- Deployed Linux VM
<img width="1918" height="852" alt="2 3  vm deployment in different region " src="https://github.com/user-attachments/assets/3dd157ff-cb12-44e8-825f-64fb1a85b6d4" />

- Configured SSH (port 22) to allow public access (0.0.0.0/0) to simulate a common cloud misconfiguration
<img width="1916" height="852" alt="2 4  vm nsg" src="https://github.com/user-attachments/assets/a0b2d41e-9f6e-45c3-a083-451ff1c7d463" />

## Initial Security Issue
This configuration exposes the VM to potential brute-force attacks and unauthorized access attempts from the public internet.
- SSH (port 22) is open to 0.0.0.0/0 (public access)

<img width="1918" height="927" alt="3  Using ssh to connect the vm" src="https://github.com/user-attachments/assets/2313943d-718d-4fe9-bf67-f459684737a2" />

  <img width="737" height="512" alt="3  Using putty to connect the vm" src="https://github.com/user-attachments/assets/4f4261e8-f450-41a9-91df-76c0599c4511" />

## Challenges & Resolutions

### Issue: Azure Deployment Failure due to Region Policy
During initial deployment, resource creation failed because Azure subscription policies restricted the allowed regions.

### Root Cause
The Azure for Students subscription enforces policies that limit which regions resources can be deployed in.

### Resolution
- Switched deployment to an allowed region (e.g., Australia Southeast / East US), in this case I used Asia East
- Standardized all resources within the permitted region

### Key Learning
Cloud environments often enforce policy constraints. Understanding and adapting to these restrictions is critical in real-world deployments.

## Architecture
The architecture diagram and technical explanation for the environment are available here:
- [Architecture Documentation](Architecture.md)

## Setup Steps
(To be added)

## Security Issues Identified
(To be added)

## Mitigations Applied
(To be added)

## Detection & Monitoring
(To be added)

## Incident Response
(To be added)
