# SSH Brute-Force Detection & Response using Wazuh

A cybersecurity lab project for detecting, investigating, and responding to SSH brute-force attacks using Wazuh, Kali Linux, Ubuntu Server, and UFW.

## Lab Architecture

| Machine | Role | OS | IP |
|---|---|---|---|
| Kali Linux | Attacker | Kali 2026.1 | 192.168.56.102 |
| secops-server | Target + Wazuh agent | Ubuntu Server | 192.168.56.101 |
| wazuh-server | SIEM (manager, indexer, dashboard) | Wazuh v4.14.8 OVA | 192.168.56.104 |

All three VMs run on a VirtualBox host-only network, isolated from the internet.

## What I Did

1. Built and verified connectivity between all three VMs (`ping`).
2. Checked SSH configuration on the target (`sshd -T`).
3. Simulated failed SSH logins from Kali against Ubuntu (invalid user + valid user, wrong password).
4. Collected the resulting events in `/var/log/auth.log` on Ubuntu.
5. Confirmed the Wazuh agent forwarded the logs and the manager raised alerts.
6. Analysed the alerts in the Wazuh dashboard (Threat Hunting → Events), mapped to MITRE ATT&CK (Brute Force, Password Guessing).
7. Blocked the attacker IP with UFW (`ufw deny from 192.168.56.102 to any port 22`).
8. Verified the block — a new SSH attempt from Kali returned `Connection refused`.
9. Documented the incident with a full report and evidence screenshots.

## Key Result

Wazuh detected the brute-force attempts, traced them to a single source IP, and the block was confirmed effective — attack contained before any compromise.

## Tools Used

VirtualBox · Kali Linux · Ubuntu Server · OpenSSH · Wazuh SIEM · UFW · MITRE ATT&CK framework

## Contents

- `SSH_BruteForce_Project_Presentation.pdf` — full project write-up (flowchart, evidence, blocking & documentation criteria, incident report)

## Author

**Sameeha** — Final-Year BCA (Cybersecurity Specialization), Brocamp Cybersecurity Specialization Program
[GitHub](https://github.com/SAMEEHASHAJAHAN) · [LinkedIn](https://linkedin.com/in/sameeha-shajahan-4582093b8)
