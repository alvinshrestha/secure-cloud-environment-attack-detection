# Setup Steps

## Objective
This document outlines the initial deployment steps used to create the Azure environment for the **Secure Cloud Environment with Attack Detection (Azure)** project.

---

## 1. Create Azure Resource Group
A resource group was created to logically organize all cloud resources for the lab.

### Configuration
- **Resource Group Name:** `rg-security-lab-2`
- **Region:** `Australia Southeast` *(or the region used successfully)*

### Outcome
This resource group serves as the main container for the project resources.

---

## 2. Deploy Linux Virtual Machine
A Linux virtual machine was deployed to serve as the primary host for security hardening, monitoring, and attack simulation.

### Configuration
- **Virtual Machine Name:** `vm-linux-sec`
- **Operating System:** Ubuntu 22.04 LTS
- **VM Size:** `B2ats_v2`
- **Authentication Type:** Password
- **Public IP:** Enabled

### Outcome
The Linux VM provides the compute environment for security configuration and testing.

---

## 3. Configure Public SSH Access (Initial State)
SSH access was enabled to allow remote administrative access to the virtual machine.

### Configuration
- **Port:** `22`
- **Protocol:** TCP
- **Source:** `Any (0.0.0.0/0)`

### Security Note
This configuration was intentionally left insecure to simulate a common cloud misconfiguration for later remediation.

### Outcome
The VM became remotely accessible over SSH from the public internet.

---

## 4. Connect to the Virtual Machine
Remote access to the VM was verified using SSH and PuTTY.

### Methods Used
- SSH via terminal
- PuTTY client

### Example SSH Command
```bash
ssh azureuser@<public-ip>
