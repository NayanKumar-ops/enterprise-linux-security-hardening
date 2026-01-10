# Linux Bastion Host Hardening

# Security Hardening Technical Report

1. Executive Summary

This project demonstrates the hardening of a Linux bastion host exposed to an untrusted network.
A bastion host serves as a controlled access point to internal systems and is therefore a high-value attack target.

The system was secured by restricting network exposure, hardening SSH access, and validating security improvements using Nmap scans.
The results show a clear reduction in attack surface and improved resistance to brute-force and reconnaissance attempts.

2. What Is a Bastion Host?

A bastion host is a publicly reachable server used to securely access private infrastructure.
Because it is exposed to the internet, it must be:

Minimal in services

Strictly firewall-controlled

Continuously validated

Any misconfiguration in a bastion host can lead to full infrastructure compromise.

3. Threat Model

The following realistic threats were considered:

SSH brute-force attacks

Network reconnaissance using port scanning

Abuse of exposed services

Repeated unauthorized access attempts

The attacker is assumed to have network-level access only, simulating an external attacker.

4. Lab Environment
Component	Details
Operating System	Rocky Linux
Firewall	firewalld
SSH Service	OpenSSH
Validation Tool	Nmap
Environment	Virtualized lab
5. Initial Exposure Assessment (Before Hardening)

An Nmap scan was performed from an external system to identify exposed ports and services.

Findings

SSH port was reachable

Firewall restrictions were minimal

No rate limiting was in place

System was vulnerable to brute-force attempts

Evidence

6. Hardening Strategy

A defense-in-depth approach was used:

Restrict inbound network access

Allow only required services

Harden SSH against brute-force attacks

Validate changes through scanning

7. Firewall Hardening

Firewalld was configured to strictly control inbound traffic.

Actions Taken

Verified active firewall zone

Allowed SSH service explicitly

Blocked all unnecessary inbound ports

Applied rich rules for connection control

Verification Commands
firewall-cmd --list-all
firewall-cmd --list-rich-rules

Evidence

8. SSH Rate Limiting

SSH rate limiting was implemented using firewalld rich rules to mitigate brute-force attacks.

Objective

Limit repeated SSH connection attempts from the same IP address.

Security Impact

Brute-force attempts are throttled or dropped

Legitimate administrative access remains functional

Attack surface is significantly reduced

Evidence

9. Post-Hardening Validation (After Hardening)

A second Nmap scan was performed after applying all hardening controls.

Results

Reduced exposed services

Improved resistance to scanning

Firewall and SSH protections confirmed

Evidence

10. Comparative Security Analysis
Security Area	Before Hardening	After Hardening
Firewall enforcement	Weak	Strict
SSH protection	None	Rate-limited
Attack surface	Broad	Reduced
Security posture	Vulnerable	Hardened
11. Lessons Learned

Bastion hosts must expose only essential services

Firewalls provide the first and strongest layer of defense

SSH rate limiting is a simple but effective control

Validation is critical to confirm security effectiveness

12. Conclusion

This project demonstrates practical Linux bastion host hardening using industry-standard tools.
By combining firewall restrictions, SSH rate limiting, and validation through scanning, the system’s exposure to common attacks was significantly reduced.

These techniques align with security practices used in enterprise and cloud environments.
