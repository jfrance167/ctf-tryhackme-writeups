# TryHackMe: Introduction to SIEM

**Room status:** in progress — tasks 1–5 completed during this session  
**Focus:** centralized logging, normalization, correlation, detection rules, and alert triage

## Verified room answers and reasoning

| Question | Answer | Why |
| --- | --- | --- |
| What does SIEM stand for? | Security Information and Event Management System | The platform's definition of a centralized security logging and analysis solution. |
| Registry-related activity | Host-centric | Registry events originate on an endpoint. |
| VPN-related activity | Network-centric | VPN activity concerns communication to or across the network. |
| Linux HTTP log location | `/var/log/httpd` | The room identifies this as an HTTP request/response and error-log location. |
| Event ID generated when event logs are removed | `104` | Windows logs Event ID 104 when event logs are cleared. |
| Alert type that may require tuning | False Positive | A non-malicious match may show a detection rule needs refinement. |

## SIEM pipeline

```text
Endpoints, servers, web services, firewalls
                  |
                  v
          collection / forwarding
                  |
                  v
     parsing + normalization + enrichment
                  |
                  v
        correlation + detection rules
                  |
                  v
         analyst triage and response
```

## Why each stage matters

- **Collection:** centralizes otherwise scattered endpoint and network evidence.
- **Normalization:** turns different vendor log formats into consistent fields such as `user`, `host`, `source_ip`, `event_id`, and `process`.
- **Correlation:** identifies a pattern that isolated events cannot reveal, such as a new VPN login followed by unusual file access and a suspicious process.
- **Detection:** expresses known risky behavior as testable rules.
- **Triage:** determines whether an alert is a true positive, false positive, or needs more evidence.

## Detection-rule example

```text
IF log_source = WinEventLog
AND event_id = 104
THEN alert = "Windows event log cleared"
```

The rule targets a potentially suspicious action because attackers may clear logs to reduce forensic visibility. It is an investigation trigger, not proof of malicious intent: administrators can also legitimately clear logs.

## Mitigations and operational improvements

- Forward critical logs off-host to prevent a compromised system from becoming the sole evidence store.
- Restrict and monitor log-clearing privileges.
- Add baseline context for accounts, hosts, and normal network destinations.
- Tune detections from analyst feedback, especially verified false positives.
- Retain raw events long enough to reconstruct incident timelines.

## Remaining lab evidence

Task 6 uses a static SIEM dashboard. When completing it, capture a redacted screenshot of the generated alert, the matching event, the rule condition, and the selected response action. Do not commit the room flag.
