# Architecture Diagram

![Architecture Diagram](Architecture-Diagram<img width="3371" height="1992" alt="Architecture-diagram" src="https://github.com/user-attachments/assets/c68d52b8-5de3-4871-b386-f470a6e2a0dc" />
)

## Overview
This architecture represents the initial deployment of the Secure Cloud Environment with Attack Detection project in Microsoft Azure.

## Components
- **Internet** – Represents public external access
- **Public IP** – Provides internet-reachable access to the virtual machine
- **Network Security Group (NSG)** – Controls inbound and outbound traffic rules
- **Virtual Network (VNet)** – Provides private network segmentation within Azure
- **Subnet** – Logical subdivision of the virtual network
- **Linux Virtual Machine (Ubuntu)** – Main compute resource used for deployment, hardening, monitoring, and attack simulation

## Initial Traffic Flow
The initial configuration allows:
- Public internet access to the VM
- SSH (Port 22) access from any source (`0.0.0.0/0`)

## Security Concern
Allowing SSH from any source creates a significant attack surface and exposes the VM to:
- Brute-force login attempts
- Unauthorized access attempts
- Public scanning and reconnaissance

## Planned Security Improvements
This architecture will be improved in later stages by:
- Restricting SSH access to trusted IPs only
- Applying host-based hardening
- Enabling centralized logging and monitoring
- Configuring attack detection and alerting
