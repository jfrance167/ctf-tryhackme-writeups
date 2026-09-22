# TryHackMe: HTTP in Detail

**Room status:** completed  
**Focus:** HTTP(S), methods, status codes, headers, cookies, and request inspection

## Request-analysis methodology

1. Identify the **method**, path, query parameters, headers, cookies, and body.
2. Inspect the **response status** and headers before interpreting the body.
3. Compare an unauthenticated request with an authenticated request in the authorized lab.
4. Identify which security decision is being made server-side, rather than assuming the browser UI enforces it.

## Minimal evidence capture

```bash
curl -i http://<THM_TARGET_IP>/
curl -I http://<THM_TARGET_IP>/
```

`-i` includes response headers with the response body. `-I` requests headers only, which is useful for quickly checking redirects, cookies, content type, and security headers without downloading the full page.

## Security-relevant observations

| Component | What to inspect | Defensive expectation |
| --- | --- | --- |
| Method | GET, POST, PUT, DELETE usage | Reject unsupported methods; authorize state changes |
| Status code | 200, 301/302, 401, 403, 404, 500 | Avoid disclosing sensitive details in errors |
| Cookies | `Secure`, `HttpOnly`, `SameSite` attributes | Protect session tokens from transport and script exposure |
| Headers | CSP, HSTS, frame protections, content type | Reduce browser-side attack surface |
| Inputs | URL and request-body parameters | Validate and encode server-side |

## Mitigations

- Enforce HTTPS and HSTS for authenticated applications.
- Set session cookies with `Secure`, `HttpOnly`, and an appropriate `SameSite` value.
- Authorize every request on the server, including direct requests to hidden routes.
- Apply a Content Security Policy and strict content types.
- Log request metadata and authorization failures without recording secrets.

## Screenshot checkpoints

- Redacted request/response pair in browser developer tools or Burp Suite.
- Cookie attributes for a test session with the session value obscured.
- Security-header result from an authorized lab request.
