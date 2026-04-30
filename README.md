# Secure Cloud Environment with Attack Detection (Azure)

## Overview
This project demonstrates the design, deployment, and security hardening of a cloud environment in Microsoft Azure, including attack detection and monitoring capabilities. 

The environment was built under Azure subscription constraints, requiring adaptation to policy-enforced region restrictions and resource limitations. These constraints reflect real-world cloud scenarios where engineers must design secure systems within operational boundaries.

The project focuses on identifying misconfigurations, applying security controls, implementing logging and alerting, and simulating attack scenarios to validate detection and response mechanisms.

---

## Objectives
- Deploy a cloud-based VM
- Identify security misconfiguration
- Apply security hardening techniques
- Implement logging and monitoring
- Simulate and detect attacks.

---

## Initial Setup
- Created Resource Group
![Resource Group](./Images/Resource-Group.png)

- Deployed Linux VM
![Deployed Linux](./Images/Deployed-Linux.png)

- Configured SSH (port 22) to allow public access (0.0.0.0/0) to simulate a common cloud misconfiguration
![SSH Missconfiguration](./Images/SSH-Missconfiguration.png)

---

## Initial Security Issue
This configuration exposes the VM to potential brute-force attacks and unauthorized access attempts from the public internet.
- SSH (port 22) is open to 0.0.0.0/0 (public access)
![SSH Login](./Images/SSH-Login.png)

---

## Challenges & Resolutions

### Issue: Azure Deployment Failure due to Region Policy
During initial deployment, resource creation failed because Azure subscription policies restricted the allowed regions.

### Root Cause
The Azure for Students subscription enforces policies that limit which regions resources can be deployed in.

### Resolution
- Switched deployment to an allowed region (e.g., Australia Southeast / East US), in this case I used Asia East
- Standardized all resources within the permitted region

### Issue: SSH Password Login Remained Enabled After Configuration Change
During hardening, password-based SSH login remained active even after updating the main SSH configuration file.

### Root Cause
The main SSH daemon configuration was being overridden by additional configuration files loaded from `/etc/ssh/sshd_config.d/`.

### Resolution
- Audited the full SSH configuration
- Identified the override file
- Updated the effective SSH authentication settings
- Verified the final applied configuration using SSH diagnostic commands

### Key Learning
- Cloud environments often enforce policy constraints. Understanding and adapting to these restrictions is critical in real-world deployments.

- Cloud-hosted Linux systems may use layered SSH configuration files. Secure hardening requires validation of the effective runtime configuration, not just the main config file.

---

## Architecture
The architecture diagram and technical explanation for the environment are available here:
- [Architecture Documentation](/1.Architecture/architecture.md)

## Setup Steps
- [Setup Steps](./2.Setup/Setup-steps.md)

## Security Issues Identified
- [Security Issues Identified](./3.Security/1.identified-issues.md)

## Mitigations Applied
- [Security Hardening](./3.Security/2.hardening-steps.md)

## Monitoring
- [Monitoring Logs](./4.Monitoring/i.Log-setup.md)

## Alerting 
- [Alerting Rules](./5.Alerting/1.alert-rule.md)
- [Limitations](./5.Alerting/2.Limitations.md)

## Attack Simulation
- [Attack Simulation](./6.AttackSimulation/AttackSimulation.md)
- [Incident Response](./6.AttackSimulation/IncidentResponse.md)

---

## Project Roadmap

- [x] Day 1: Azure environment deployment
- [x] Day 1: Initial security misconfiguration identified
- [x] Day 1: SSH connectivity verified
- [x] Week 2: Linux VM hardening
- [x] Week 3: Azure NSG restriction and network hardening
- [x] Week 4: Identity and Access Management (RBAC)
- [x] Week 5: Logging and monitoring with Azure Monitor / Log Analytics
- [x] Week 6: Alerting and detection rule creation
- [x] Week 7: Attack simulation and evidence collection
- [x] Week 8: Final documentation and interview demo preparation

---

## Skills Demonstrated

### Cloud & Infrastructure
- Microsoft Azure resource deployment and configuration
- Virtual machine provisioning and access management
- Azure subscription policy navigation and constraint resolution

### Security Engineering
- Cloud misconfiguration identification and remediation
- Network Security Group (NSG) design and hardening
- SSH hardening — key-based auth, config layering, daemon management
- Identity and Access Management (RBAC — least privilege)
- Linux remote administration and security configuration

### Monitoring & Detection
- Azure Log Analytics workspace configuration
- Data Collection Rule (DCR) design and troubleshooting
- KQL (Kusto Query Language) — detection query writing and tuning
- Azure Monitor alert rule engineering
- False positive analysis and alert tuning
- End-to-end monitoring pipeline validation

### Attack Simulation & Response
- SSH brute force simulation using Hydra
- MITRE ATT&CK mapping (T1110.001 — Brute Force)
- Log-based attack detection and evidence collection
- Structured incident response (NIST SP 800-61 framework)

### Professional Practices
- Security-focused technical documentation
- GitHub portfolio development
- Real-world troubleshooting under cloud constraints
