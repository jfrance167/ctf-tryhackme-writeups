# Security policy

This repository contains authorized security-lab documentation. It has no supported production release or security-service guarantee.

## Reporting a concern

Report suspected exposed credentials or a security issue privately using this repository's GitHub private vulnerability reporting feature if available. Otherwise contact the owner through the GitHub profile to arrange a private channel before sharing sensitive details. Do not put secrets, personal data, or exploit evidence in a public issue.

Include the affected path and commit, expected versus observed behavior, and a minimal sanitized reproduction. Never test systems without their owner's explicit authorization.

## Safe reuse

Review historical configuration and current platform requirements before reuse. Use an isolated environment you own, synthetic data, least privilege, and a teardown plan. Public examples and private containers do not by themselves establish network isolation. Store credentials outside Git; an ignore rule does not remove already committed material. No compliance certification is claimed.
