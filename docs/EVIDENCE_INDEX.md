# Evidence Index

This index lists the sanitized evidence intended for publication. Numerical internal IP addresses have been black-boxed in screenshots where they were visible.

## Phase 1 — Baseline

| File | Purpose |
|---|---|
| [`wazuh-endpoint-overview.png`](../evidence/01-baseline/wazuh-endpoint-overview.png) | Wazuh endpoint overview and final dashboard state |
| [`sca-initial-baseline-45-percent.png`](../evidence/01-baseline/sca-initial-baseline-45-percent.png) | Initial SCA baseline: 45%, 86 passed, 102 failed, 19 N/A |
| [`sca-baseline-control-list.png`](../evidence/01-baseline/sca-baseline-control-list.png) | Initial SCA control-level view |

## Phase 2 — Vulnerability Management

| File | Purpose |
|---|---|
| [`vulnerability-inventory.png`](../evidence/02-vulnerability-management/vulnerability-inventory.png) | Vulnerability inventory used during final documentation |
| [`running-kernel-verification.png`](../evidence/02-vulnerability-management/running-kernel-verification.png) | Endpoint running-kernel verification |
| [`vulnerability-summary-intermediate.png`](../evidence/02-vulnerability-management/vulnerability-summary-intermediate.png) | Intermediate vulnerability severity state |
| [`vulnerability-summary-final.png`](../evidence/02-vulnerability-management/vulnerability-summary-final.png) | Final retained vulnerability severity state |

## Phase 3 — Security Hardening

| File | Purpose |
|---|---|
| [`sca-33168-macs-failed.png`](../evidence/03-security-hardening/sca-33168-macs-failed.png) | MAC hardening control before remediation |
| [`sca-33168-macs-passed.png`](../evidence/03-security-hardening/sca-33168-macs-passed.png) | MAC hardening control after remediation |
| [`ssh-hardening-configuration.png`](../evidence/03-security-hardening/ssh-hardening-configuration.png) | SSH hardening configuration |
| [`ssh-effective-configuration.png`](../evidence/03-security-hardening/ssh-effective-configuration.png) | Effective `sshd -T` verification |
| [`sca-33161-forwarding-passed.png`](../evidence/03-security-hardening/sca-33161-forwarding-passed.png) | DisableForwarding control passed |
| [`sca-33300-failed.png`](../evidence/03-security-hardening/sca-33300-failed.png) | Shadowed-password SCA control remained failed |
| [`sca-33300-pwck-validation.png`](../evidence/03-security-hardening/sca-33300-pwck-validation.png) | Supplemental manual account-database validation |
| [`hermes-legacy-account.png`](../evidence/03-security-hardening/hermes-legacy-account.png) | Legacy account and SSH authorization evidence |
| [`sca-final-score-49-percent.png`](../evidence/03-security-hardening/sca-final-score-49-percent.png) | Final SCA state: 49%, 93 passed, 95 failed, 19 N/A |

## Phase 4 — File Integrity Monitoring

| File | Purpose |
|---|---|
| [`fim-etc-realtime-validation.png`](../evidence/04-file-integrity-monitoring/fim-etc-realtime-validation.png) | Earlier real-time FIM validation under `/etc` |
| [`fim-demo-event-list.png`](../evidence/04-file-integrity-monitoring/fim-demo-event-list.png) | Controlled FIM event list |
| [`fim-modification-integrity-fields.png`](../evidence/04-file-integrity-monitoring/fim-modification-integrity-fields.png) | Integrity metadata for controlled modification |
| [`fim-modification-diff-no-to-yes.png`](../evidence/04-file-integrity-monitoring/fim-modification-diff-no-to-yes.png) | Line-level modification diff |
| [`fim-modification-sha256.png`](../evidence/04-file-integrity-monitoring/fim-modification-sha256.png) | Modification SHA-256 before/after values |
| [`fim-restoration-diff-yes-to-no.png`](../evidence/04-file-integrity-monitoring/fim-restoration-diff-yes-to-no.png) | Restoration diff |
| [`fim-restoration-sha256.png`](../evidence/04-file-integrity-monitoring/fim-restoration-sha256.png) | Restoration SHA-256 before/after values |

## Phase 5 — SSH Detection

| File | Purpose |
|---|---|
| [`ssh-initial-security-events.png`](../evidence/05-ssh-detection/ssh-initial-security-events.png) | Early SSH/sudo security-event examples |
| [`rule-5716-event-details.png`](../evidence/05-ssh-detection/rule-5716-event-details.png) | Failed-public-key authentication event |
| [`failed-publickey-full-log.png`](../evidence/05-ssh-detection/failed-publickey-full-log.png) | Focused sanitized SSH raw-log excerpt |
| [`rule-100120-correlation-event-list.png`](../evidence/05-ssh-detection/rule-100120-correlation-event-list.png) | Event list showing custom correlation |
| [`rule-100120-event-details.png`](../evidence/05-ssh-detection/rule-100120-event-details.png) | Custom rule details: level, frequency, MITRE mappings |

## Phase 6 — Active Response

| File | Purpose |
|---|---|
| [`firewall-drop-host-blocked-event.png`](../evidence/06-active-response/firewall-drop-host-blocked-event.png) | Wazuh `Host Blocked by firewall-drop Active Response` event after rule 100120 |

## Publication notes

- Redundant alternate screenshots and exact duplicates are intentionally excluded from the public repository.
- Raw working notes are intentionally excluded from the public repository because they contain unsanitized internal addressing and drafting material.
- The final project documentation and sanitized evidence are the authoritative publication set.
