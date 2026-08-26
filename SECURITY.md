# Security and Disclosure Policy

## Purpose

This repository is a sanitized portfolio. It documents engineering patterns while intentionally withholding details that would make the live environment easier to discover or target.

## Public documentation rules

Do not commit:

- public or private IP addresses;
- internal hostnames, domains, subdomains, ports, or VPN routes;
- VLAN identifiers or exact firewall and reverse-proxy rules;
- administrative URLs or screenshots of administrative interfaces;
- usernames, personal email addresses, phone numbers, platform IDs, or device identifiers;
- tokens, keys, passwords, cookies, QR codes, recovery material, or secret-bearing configuration;
- live Compose files, environment files, inventories, backups, databases, logs, or exports;
- exact software versions from the live environment unless disclosure is deliberate and reviewed.

Public diagrams use capability labels and generalized boundaries. The real inventory and recovery material remain in private, access-controlled systems.

## Repository checks

Before publication, scan independently:

1. working tree;
2. exact Git index;
3. reachable commit history;
4. Git object database health;
5. a fresh clone from the public remote.

The included scanner detects common indicators and supports a gitignored local marker file for operator-specific labels.

## Reporting a problem

If you find a credential, identifier, or infrastructure detail that should not be public, use GitHub's private vulnerability-reporting or security-advisory channel for this repository. Do not repost the value in a public issue.

## Scope

This repository does not expose a runnable service and does not accept credentials or owner enrollment data. Security reports should concern the repository's published content, examples, scanner, or disclosure boundary.
