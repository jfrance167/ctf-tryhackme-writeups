# CTF & TryHackMe Writeups

Portfolio-oriented walkthroughs for completed TryHackMe training rooms and packet-analysis practice. Each writeup explains the investigative sequence, why a technique was chosen, the evidence it produces, and the defensive lesson.

> Scope: all offensive examples are limited to TryHackMe-provided, intentionally vulnerable training targets. Do not reuse commands against systems without explicit authorization.

## Completed-room notes

| Writeup | Focus | Status |
| --- | --- | --- |
| [Offensive Security Intro](tryhackme/offensive-security-intro.md) | Web reconnaissance and authentication weaknesses | Documented from completed room |
| [Defensive Security Intro](tryhackme/defensive-security-intro.md) | Detect, contain, investigate, report | Documented from completed room |
| [Introduction to SIEM](tryhackme/introduction-to-siem.md) | Log sources, correlation, alert triage | In progress; first five tasks completed |
| [HTTP in Detail](tryhackme/http-in-detail.md) | HTTP requests, responses, headers, and cookies | Documented from completed room |
| [Search Skills](tryhackme/search-skills.md) | OSINT source selection and validation | Documented from completed room |
| [Packet Analysis Playbook](packet-analysis/ettercap-and-wireshark.md) | Ethical packet capture and analysis workflow | Reusable lab methodology |

## Repository conventions

- `tryhackme/` contains room-specific notes.
- `packet-analysis/` contains reusable packet-analysis methodology.
- `assets/` is reserved for redacted screenshots captured during future lab runs.

![SIEM evidence pipeline](assets/siem-pipeline.svg)

![Authorized web-assessment workflow](assets/web-assessment-flow.svg)

No screenshots have been copied from the platform into this repository. The writeups include explicit screenshot checkpoints instead of fabricated evidence. Add only screenshots you personally captured in an authorized lab, and redact usernames, target addresses, tokens, flags, and session material before committing.

## Recommended evidence format

```text
assets/<room-slug>/01-<short-description>.png
```

Then embed it with descriptive alt text:

```md
![Redacted HTTP response headers](../assets/http-in-detail/01-response-headers.png)
```
