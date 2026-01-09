Enterprise Linux Server Hardening & Security Audit

 Executive Summary
This project demonstrates the hardening of an Enterprise Linux server (Rocky Linux 9) to mitigate network-based attacks. The objective was to reduce the attack surface by moving from a default "open" state to a "Least Privilege" network posture using native kernel-level firewalling.


The project simulates a real-world Red Team vs. Blue Team scenario:
Red Team (Audit): Executing external network scans to identify vulnerabilities.
Blue Team (Defense): Implementing Rich Rules, Rate Limiting, and Zone Management using firewalld without relying on external dependencies.


Architecture & Environment
Target Server (Blue Team): Rocky Linux 9 (Enterprise Kernel)
Attacker Node (Red Team): External Host via PowerShell (Nmap)
Security Framework: firewalld (Dynamic Firewall Manager)
Network Config: Host-Only Adapter (Isolated Lab Network: 192.168.56.0/24)


Phase 1: Vulnerability Assessment (Before Hardening)
Objective: Establish a baseline security posture.
An external Nmap audit was conducted to identify exposed services and potential entry points.
Command Executed (Attacker): *nmap 192.168.56.101*
Findings:
 Critical Risk: Port 80 (HTTP) Open and Unsecured.
 Risk: Port 22 (SSH) Open to all IPs without restriction.



🛡️ Phase 2: Defense Implementation (Hardening)
Objective: Implement "Defense in Depth" using Enterprise Firewall policies.


1. Zero Trust Implementation
Switched default firewall zone to DROP. This ensures that any traffic not explicitly allowed is silently discarded, adhering to the principle of "Deny by Default."

2. Native SSH Brute-Force Mitigation (Rich Rules)
Instead of installing heavy external tools, I utilized Firewalld Rich Rules to enforce rate-limiting directly at the firewall level. This rejects attackers attempting brute-force login attacks (more than 4 attempts/minute).

Configuration Applied:# Set Default Zone to Drop (Block all)
sudo firewall-cmd --set-default-zone=drop

# Apply Native SSH Rate Limiting
# Rule: Accept SSH, but limit to 4 new connections per minute.
sudo firewall-cmd --permanent --add-rich-rule='rule service name="ssh" limit value="4/m" accept'

# Reload Firewall to Apply
sudo firewall-cmd --reload


Phase 3: Verification Audit (After Hardening)
Objective: Verify that the attack surface has been neutralized.
A second Nmap scan was executed from the external attacker node.

Result:
 Port 80 (HTTP): Filtered/Blocked (Invisible to scanner).
 Port 22 (SSH): Open but protected by Rate Limiting.
 
 # Stealth Scan: The server correctly drops unauthorized ICMP packets.



 Key Skills Demonstrated
Network Security: Port auditing and attack surface reduction.
System Administration: Advanced firewalld configuration on RHEL-based systems.
Traffic Shaping: Implementing Rate Limiting to stop automated bot attacks.
Security Auditing: Using Nmap for "Proof of Secure" validation.



Author: Nayan




