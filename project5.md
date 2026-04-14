[Back to Portfolio](./)

Endpoint Security Project
==========================

-   **Class:** CSCI 352 – Cyber Defense
-   **Grade:** In Progress
-   **Language(s):** Bash / Linux CLI
-   **Collaborators:** Kailey Owens, Logan Riley

## Project Description

The Endpoint Security Project was a hands-on lab completed as part of CSCI 352 – Cyber Defense. The goal was to set up and harden a Linux (Ubuntu) endpoint inside a virtual machine, demonstrating core security practices used by system administrators and cybersecurity professionals.

The project covered six critical areas of endpoint security: user account management, system updates and patch management, password policy enforcement, file encryption using eCryptfs, file permission hardening with `chmod` and `chown`, and firewall configuration using UFW (Uncomplicated Firewall).

All tasks were performed inside an Ubuntu virtual machine running on Oracle VirtualBox, simulating a real-world environment where an administrator needs to secure a freshly deployed Linux system.

## Security Tasks Completed

### Part 1 — User Management & Password Security
Created new user accounts and demonstrated the difference between default passwords and strong, manually-set passwords to prevent unauthorized access.

### Part 2 — System Updates & Patch Management
Updated all system packages using `apt update`, `apt upgrade`, and `apt autoremove` to ensure the system was patched against known vulnerabilities.

### Part 3 — Password Policy Enforcement
Installed `libpwquality-tools` and configured system-wide password policies requiring:
- Minimum 10 characters
- At least 1 digit, 1 uppercase letter, 1 lowercase letter, and 1 special character

Verified that weak passwords were rejected when tested under a non-root user.

### Part 4 — File Encryption with eCryptfs
Created an encrypted directory using eCryptfs. Files inside the directory were accessible only when the encryption layer was mounted, demonstrating data-at-rest protection.

### Part 5 — File Permissions (chmod & chown)
Created sensitive files and restricted access using `chmod 600` (owner read/write only). Changed file ownership using `chown` to control which users could access specific files.

### Part 6 — Firewall Configuration with UFW
Enabled and configured UFW with:
- Default deny all incoming traffic
- Default allow all outgoing traffic
- Allowed SSH (port 22) for remote administration

## Tools & Technologies Used

| Tool | Purpose |
|------|---------|
| Oracle VirtualBox | Virtual machine hypervisor |
| Ubuntu Desktop | Target operating system |
| UFW | Uncomplicated Firewall for network security |
| eCryptfs | Encrypted filesystem for data protection |
| libpwquality | Password complexity enforcement |
| chmod / chown | File permission and ownership management |

## Additional Considerations

This project reinforced the importance of defense-in-depth — layering multiple security controls so that if one fails, others still protect the system. Each task addressed a different attack vector: weak passwords, unpatched software, unencrypted data, overly permissive file access, and open network ports. Together, these practices form the foundation of endpoint hardening used in enterprise security environments.

[Back to Portfolio](./)
