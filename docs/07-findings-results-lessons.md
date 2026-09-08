# 9. Troubleshooting and Investigation Highlights

I exclude minor setup mistakes from this report and focus on troubleshooting that changed the security analysis.

## Vulnerability findings persisted after package/kernel changes

I did not assume that a newer running kernel meant Wazuh should immediately clear every related vulnerability. I compared package inventory, runtime kernel state, and available fix information and retained unresolved findings for monitoring.

## SCA 33300 disagreed with manual validation

Rather than changing `/etc/passwd` solely to satisfy a scanner result, I manually inspected the password-field condition. The direct check returned no non-shadowed entries, and `pwck -r` made no database changes. I documented the Wazuh result as a disputed scanner finding because the endpoint condition I tested did not reproduce the reported failure.

## Existing SSH correlation did not fit the hardened endpoint

The endpoint generated `Failed publickey` events. The response path I wanted did not trigger from the built-in rule path I reviewed, so I created a custom correlation rule around the actual log event instead of weakening SSH.

## Active Response required end-to-end validation

I verified the chain at multiple points:

- rule `5716` detected the individual authentication failures,
- rule `100120` correlated repeated failures,
- Wazuh generated the `Host Blocked by firewall-drop Active Response` event,
- and SSH access later returned after the temporary response window.

---

# 10. Key Findings

## Vulnerability counts require context

A large SIEM vulnerability count is not the same thing as a large number of proven exploitation paths. Package state, runtime state, available fixes, and endpoint role all matter.

## Runtime verification does not erase package findings

The endpoint was running a newer kernel than the originally reported vulnerable package, but Wazuh continued reporting selected findings. I kept them visible instead of tuning them away.

## Scanner results require validation

SCA `33300` is the clearest example in this project. The Wazuh result remained failed, but the manual condition check did not reproduce the reported endpoint condition, so I did not make an unnecessary configuration change.

## Security review can uncover unrelated access risks

The legacy `hermes` account and SSH authorization were discovered during account/security review. It remains a documented cleanup item.

## Hardening and detection engineering are connected

Because password authentication was disabled, the relevant event was `Failed publickey`. Detection logic had to match the hardened endpoint's actual telemetry.

## Effective configuration matters

`sshd -T` provided stronger verification than showing only the configuration file.

## FIM can provide content-level evidence

With `report_changes` enabled, Wazuh recorded the exact changed line as well as the integrity hashes.

## Response should be verified independently

The strongest Active Response evidence was the combination of the custom correlation alert, Wazuh's host-blocked event, and the observed SSH behavior.

---

# 11. Final Results

| Capability | Result |
|---|---|
| Wazuh server deployment | Completed |
| Debian endpoint onboarding | Completed |
| Endpoint baseline | Completed |
| Vulnerability investigation | Completed |
| Selected kernel CVEs fully cleared | Not claimed; retained for monitoring |
| Initial SCA baseline | 45% — 86 passed / 102 failed / 19 N/A |
| Final SCA state | 49% — 93 passed / 95 failed / 19 N/A |
| SCA 33168 | Passed |
| SCA 33161 | Passed |
| SCA 33300 | Remained failed; manual endpoint check did not reproduce the reported condition |
| SSH effective configuration | Verified with `sshd -T` |
| Legacy `hermes` account | Still present; cleanup deferred |
| Real-time FIM | Confirmed |
| FIM modification | Detected |
| FIM restoration | Detected; baseline hash restored |
| SSH failed-public-key detection | Rule 5716 confirmed |
| Custom correlation | Rule 100120 confirmed |
| Rule 100120 frequency | 3 |
| Correlation timeframe | 120 seconds |
| Active Response | `Host Blocked by firewall-drop Active Response` event confirmed |
| Active Response timeout | 60 seconds |
| SSH connectivity after timeout | Successfully restored in testing |

---

# 12. Limitations

- I used one Debian endpoint for the primary workflow.
- The endpoint is an operational homelab Docker host, so I deliberately avoided unnecessary changes.
- The selected kernel CVEs remained monitoring items rather than being claimed as fully remediated.
- The `hermes` account remains a deferred access-management cleanup item.
- I did not enable FIM `whodata` for the dedicated demonstration path.
- I did not retain a clean copy of the final custom-rule XML.
- I did not retain a Wazuh screenshot showing the unblock action.
- The SSH event was controlled testing, not a real intrusion.
- The project does not claim enterprise-scale SIEM architecture, high availability, or full SOC operations.

---

# 13. Lessons Learned

1. A SIEM finding is the start of an investigation, not the conclusion.
2. I should not change a production-like endpoint only to improve a compliance score.
3. I should keep unresolved vulnerability findings visible until I can verify remediation.
4. Package cleanup requires operational context on a service host.
5. Effective configuration should be verified after hardening.
6. Detection logic should match the logs produced by the real security configuration.
7. Detection and response should be tested as an end-to-end chain.
8. Multiple evidence sources are stronger than a single dashboard screenshot.
9. Unresolved findings should remain visible in the final report.
10. Careful evidence review matters: exact hashes, rule thresholds, and response claims should match retained artifacts.

---

# 14. Phase 7 — Portfolio and Publication

For the final phase, I reviewed the retained evidence, sanitized screenshots containing internal addresses, removed duplicate and drafting artifacts, organized the documentation in roadmap order, and prepared the repository for public portfolio use.

The publication set includes:

- a concise project README,
- a static lab architecture diagram,
- phase-by-phase technical documentation,
- an evidence index,
- sanitized screenshots grouped by roadmap phase,
- and repository ignore rules for common secret/private-key material.

I intentionally excluded raw working notes, duplicate screenshots, unsanitized internal addresses, and intermediate drafts from the public project.

### Phase 7 result

I converted the working homelab notes and retained evidence into a structured portfolio repository while preserving unresolved findings and limitations instead of presenting the project as more complete than the evidence supports.

---

# 15. Conclusion

The most valuable part of this project was not installing Wazuh. It was using the platform to work through disagreements between scanner output and endpoint state, make conservative remediation decisions, build a detection around the endpoint's actual SSH behavior, and verify an automated response.

The project demonstrates a complete single-endpoint blue-team workflow while remaining explicit about unresolved findings and evidence limitations.
