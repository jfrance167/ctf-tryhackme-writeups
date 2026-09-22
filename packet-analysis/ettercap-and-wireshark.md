# Packet Analysis Playbook: Ettercap and Wireshark

**Use only on networks and hosts you own or are explicitly authorized to test.** This playbook is intended for isolated CTF or lab traffic.

## Goal

Capture a defined traffic sample, filter it down to a question, preserve enough context to reproduce the conclusion, and recommend a control that reduces the risk.

## Workflow

1. **Define scope:** identify the lab interface, target range, time window, and hypothesis.
2. **Capture minimally:** collect only traffic needed for the exercise; avoid production credentials and unrelated user data.
3. **Filter deliberately:** begin with protocol and endpoint filters, then narrow to conversations, requests, or anomalies.
4. **Validate context:** compare packet payloads, DNS resolution, TCP stream behavior, and endpoint logs where available.
5. **Preserve findings:** note packet numbers, timestamps, filter expression, and a redacted excerpt.
6. **Mitigate:** map the observation to encryption, segmentation, authentication, monitoring, or patching controls.

## Wireshark filters

```text
dns
http.request
tcp.flags.syn == 1 && tcp.flags.ack == 0
ip.addr == <LAB_HOST_IP>
```

Each filter answers a different question: name resolution, web requests, connection attempts, or traffic associated with one scoped lab host.

## Ettercap lab use

Ettercap can demonstrate man-in-the-middle risk in an isolated lab. The meaningful documentation is not a command transcript; it is the evidence that plaintext protocols expose data and that encrypted, authenticated alternatives prevent that exposure.

## Mitigations

- Replace plaintext protocols with TLS-protected alternatives.
- Use certificate validation and HSTS where applicable.
- Segment networks and enable switch protections such as DHCP snooping and dynamic ARP inspection.
- Monitor for ARP-table changes, duplicate gateway MAC addresses, and anomalous DNS responses.

## Screenshot checkpoints

- Capture-interface and scope information with addresses redacted.
- Wireshark display filter and relevant packet list.
- Follow-stream view with credentials, tokens, and personal data redacted.
- A short findings table linking observed traffic to mitigation.
