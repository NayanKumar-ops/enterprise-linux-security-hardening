# Enterprise Linux Security Hardening

A practical security hardening project for Rocky Linux — covering firewall configuration, SSH rate-limiting, access control, and bastion host hardening. Built and tested on a real Rocky Linux minimal environment (no GUI).

---

## What This Project Covers

This repository documents hands-on Linux security hardening techniques used to reduce attack surface on production-style Linux systems.

- **Firewall hardening** — configuring firewalld rules to restrict unauthorized access
- **SSH rate-limiting** — protecting SSH from brute-force attacks
- **Access Control Lists (ACLs)** — fine-grained file and directory permission management using setfacl
- **Bastion host hardening** — securing a jump server used as the single entry point to a private network

---

## Environment

- OS: Rocky Linux (minimal install, no GUI)
- All configurations are terminal-only
- Designed to reflect real-world enterprise Linux security practices

---

## Structure

```
enterprise-linux-security-hardening/
└── linux-bastion-host-hardening/    # Hardening scripts and configs for bastion hosts
```

---

## Key Concepts Practiced

- firewalld zone management and rule configuration
- SSH daemon hardening via `/etc/ssh/sshd_config`
- Rate-limiting with firewalld rich rules
- ACL management with `setfacl` and `getfacl`
- Principle of least privilege applied to file permissions

---

## Why I Built This

I am a self-taught Linux sysadmin studying for RHCSA. I built this project to practice real security hardening techniques — not in a simulator but on an actual Rocky Linux minimal install. Every command here has been run and tested on a live system.

---

## Author

**NayanKumar-ops**.

