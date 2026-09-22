# TryHackMe: Offensive Security Intro

**Room status:** completed  
**Focus:** controlled web reconnaissance, content discovery, and weak-authentication risk  
**Environment:** TryHackMe's intentionally vulnerable FakeBank training target

## Objective

The room demonstrates a compact offensive-security workflow: identify an exposed web service, enumerate the application's visible and hidden content, validate an authentication weakness within the lab, and capture evidence for remediation.

## Methodology

1. **Establish scope.** Confirm that the IP address belongs to the assigned TryHackMe lab before interacting with it. This makes the activity authorized and keeps the testing boundary clear.
2. **Identify the web service.** Use a targeted service check to confirm the exposed HTTP service and collect basic version or title information.

   ```bash
   nmap -sV -p 80 <THM_TARGET_IP>
   ```

   `-sV` asks Nmap to identify the service; limiting the scan to the known web port keeps the test narrow and reproducible.

3. **Enumerate web content.** Request the public site first, inspect links, forms, comments, and redirects, then use a wordlist-based content discovery pass against the lab target.

   ```bash
   gobuster dir -u http://<THM_TARGET_IP>/ -w /usr/share/wordlists/dirb/common.txt -x html,php,txt
   ```

   Directory enumeration looks for unlinked but web-accessible routes. The extension list is deliberately small so that results stay relevant and noise remains manageable.

4. **Validate the finding manually.** Navigate to each discovered route and record the HTTP status, access-control behavior, and whether it reveals an administrative function. Discovery alone is not proof of a vulnerability; manual validation rules out soft-404 pages and intended public endpoints.
5. **Demonstrate the weakness only in the lab.** Follow the room's guided authentication exercise. Do not transfer credentials, wordlists, or techniques to any non-lab site.
6. **Record remediation evidence.** Capture the affected route, the expected access-control decision, and the observed behavior. Avoid storing real credentials or flags in Git.

## Tools used

| Tool | Why it was used | Evidence produced |
| --- | --- | --- |
| Browser / Burp Suite Community | Inspect requests, responses, redirects, and form behavior | Request/response evidence |
| Nmap | Confirm exposed web service | Service and port inventory |
| Gobuster | Find unlinked lab content | Candidate route list |

## Vulnerability and impact

An exposed administrative route combined with weak authentication can allow an attacker to reach privileged functions, access sensitive records, or alter application data. The underlying issue is not merely that a path is discoverable—URLs are not access controls—but that authorization and authentication are insufficiently enforced server-side.

## Mitigations

- Require strong, server-side authentication and authorization on every administrative action.
- Apply rate limiting, account lockout safeguards, and MFA where appropriate.
- Return consistent error handling for unauthorized resources; do not rely on hidden URLs.
- Monitor repeated failed logins and unusual requests to administrative routes.
- Include authenticated and unauthenticated route testing in release security checks.

## Screenshot checkpoints

Add redacted screenshots of:

1. The scoped lab target and permitted room context.
2. A filtered content-discovery result showing the relevant route.
3. The sanitized HTTP response that demonstrates access control working or failing.

## Takeaway

The useful habit is a disciplined sequence: scope first, enumerate methodically, validate manually, and translate every technical observation into a remediation action.
