# TryHackMe: Search Skills

**Room status:** completed  
**Focus:** purposeful searching, technical documentation, Shodan-style discovery, VirusTotal-style analysis, CVE research, and GitHub investigation

## Methodology

The central lesson is to select the source that can answer the question, then validate the result instead of treating search output as proof.

| Question | Appropriate source | Validation step |
| --- | --- | --- |
| Is a public service exposed? | Asset search engine / approved scanner | Confirm ownership and service evidence |
| Is a file or hash known malicious? | Malware-analysis service | Check vendor context and submission date |
| What does a CVE affect? | Vendor advisory, NVD, CNA record | Compare version and configuration |
| How does a command work? | Official manual / vendor documentation | Test only in a sandbox |
| Is public code relevant? | Source repository and release notes | Review provenance and commit history |

## Search patterns

```text
site:vendor.example "product name" advisory
"CVE-YYYY-NNNN" vendor advisory
repo:organization/project release notes
```

The purpose of operators such as `site:` and quoted phrases is precision: they reduce irrelevant hits and help locate primary sources. Search results and public code are leads, not trusted instructions.

## Defensive takeaways

- Maintain an accurate external asset inventory; public exposure should never be a surprise.
- Patch based on verified product versions and exploitation context, not CVE headlines alone.
- Treat downloaded proof-of-concept code as untrusted; analyze it in an isolated environment.
- Record source URLs, access date, and confidence level in investigation notes.

## Screenshot checkpoints

- A redacted, authorized asset-search result.
- A CVE record paired with the vendor's advisory.
- A repository history view showing provenance checks.
