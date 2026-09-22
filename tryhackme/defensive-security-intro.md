# TryHackMe: Defensive Security Intro

**Room status:** completed  
**Focus:** detection, containment, investigation, and reporting in a simulated FakeBank incident

## Incident-handling workflow

The room frames defensive security as a cycle rather than a single alert review.

```text
Alert or anomaly
  -> confirm scope and severity
  -> contain affected access or host
  -> preserve and correlate evidence
  -> eradicate and recover
  -> report lessons learned and tune detections
```

## Methodology

1. **Triage the signal.** Identify what raised concern: source IP, account, affected host, timestamp, and event type. Preserve the original time zone and log source.
2. **Scope before acting.** Search for the same user, source, process, destination, or indicator across endpoint, authentication, web, and network logs. A single event has limited meaning; a timeline supplies context.
3. **Contain proportionately.** In a real incident this could mean revoking a session, disabling a compromised account, isolating an endpoint, or blocking an observed malicious IP. Record the time and owner of every containment change.
4. **Investigate the root cause.** Compare normal behavior against observed behavior, identify the initial access path, and determine whether any credentials, data, or persistence mechanisms were affected.
5. **Report clearly.** Separate facts from assumptions, name evidence sources, state business impact, and list remediation owners and dates.

## Example investigation queries

The exact syntax differs by SIEM; the reasoning is portable.

```text
authentication events where user = <account> within ±30 minutes
network events where source_ip = <suspicious-ip>
endpoint events where hostname = <affected-host>
```

The first query establishes account activity, the second checks infrastructure exposure, and the third connects network behavior to endpoint execution.

## Defensive controls

| Risk | Control | Detection opportunity |
| --- | --- | --- |
| Stolen credentials | MFA, conditional access, session revocation | Impossible travel, new device, repeated failures |
| Malicious execution | Application allowlisting, EDR | Unusual parent/child process chains |
| Data exfiltration | Egress controls, DLP | Large or unusual outbound transfers |
| Delayed response | Documented playbooks and ownership | Time-to-triage and containment metrics |

## Screenshot checkpoints

- Alert overview with identifiers redacted.
- Correlated timeline across at least two log sources.
- Containment action or an incident report excerpt with sensitive fields removed.

## Takeaway

Defensive work succeeds when analysts preserve context: logs become actionable only when they are correlated into an explainable timeline.
