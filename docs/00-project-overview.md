# Wazuh SIEM Homelab — Project Documentation

## 1. Project objective

I built this project to demonstrate practical SIEM administration and blue-team investigation using Wazuh inside my homelab. I monitored an existing Debian Docker host rather than a disposable test system so that vulnerability and hardening decisions had to account for an endpoint that already provided services.

My workflow was:

1. Establish a baseline.
2. Review vulnerability findings.
3. Investigate selected CVEs.
4. Review and remediate selected SCA findings.
5. Configure and validate File Integrity Monitoring.
6. Generate and investigate controlled SSH authentication failures.
7. Build a custom correlation rule for repeated public-key failures.
8. Verify Wazuh Active Response.
9. Review and sanitize the evidence, document limitations and unresolved findings, and prepare the project for portfolio publication.

The goal was not to make every dashboard finding disappear. The goal was to investigate what Wazuh reported, validate the endpoint state, remediate what was appropriate, and preserve unresolved findings honestly.

---

## 2. Lab environment

### Wazuh server

| Component | Configuration |
|---|---|
| Platform | Proxmox VE |
| Operating system | Ubuntu Server 24.04 |
| Deployment | Wazuh all-in-one |
| Virtual CPU | 4 vCPU |
| Storage | 50 GB |
| Dashboard | HTTPS / TCP 443 |

### Monitored endpoint

| Field | Verified value |
|---|---|
| Agent name | `debian-docker` |
| Operating system | Debian GNU/Linux 13 (trixie) |
| Debian version | 13.6 |
| Recorded kernel | `6.12.101+deb13-amd64` |
| Wazuh agent | `4.14.7-1` |
| Agent service | `active` |

I also used a separate workstation to generate controlled remote SSH authentication events. Numerical internal IP addresses are omitted or visually redacted in the public evidence.

![Wazuh endpoint overview](../evidence/01-baseline/wazuh-endpoint-overview.png)

---
