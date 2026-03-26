# Security Issues Identified

## 1. Public SSH Exposure
SSH (port 22) was initially configured to allow access from any source (`0.0.0.0/0`), exposing the VM to the public internet.

### Risk
- Brute-force login attempts
- Unauthorized access attempts
- Public reconnaissance and scanning

## 2. Password-Based Authentication
The VM was initially configured with password-based SSH authentication, which is more vulnerable than key-based access.

### Risk
- Credential guessing
- Password brute-force attacks
- Increased exposure if credentials are weak or reused

## 3. Minimal Initial Hardening
At deployment, the VM had no host-based firewall or brute-force mitigation controls enabled.

### Risk
- Reduced resilience against common attack techniques
- Larger attack surface
