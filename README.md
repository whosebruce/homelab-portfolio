# Homelab Portfolio

**A sanitized engineering portfolio for the self-hosted infrastructure, automation, and AI-agent systems I operate.**

This repository explains the architecture, operating practices, and technical decisions behind my home lab without publishing live addresses, routes, credentials, administrative endpoints, or a complete attack-surface inventory.

> **Disclosure boundary:** this is an engineering portfolio, not a live network map. Names, quantities, placement, and connectivity are intentionally generalized.

## What the lab demonstrates

| Layer | Representative technologies | Engineering focus |
| --- | --- | --- |
| Edge and access | OPNsense, managed switching, mesh Wi-Fi, Tailscale, Cloudflare, Caddy | Segmentation, encrypted remote access, DNS, TLS, and controlled exposure |
| Compute | Proxmox VE, Linux virtual machines, Docker/Compose, GPU passthrough | Workload placement, isolation, capacity planning, and recoverability |
| Storage | TrueNAS SCALE, SMB-backed workloads, snapshots, independent backups | Data ownership, permissions, lifecycle management, and restore planning |
| AI and automation | Hermes Agent, Ollama, Open WebUI, SearXNG, Firecrawl, n8n | Role-separated agents, local/cloud model routing, research, and scheduled workflows |
| Applications | Home automation, media, DNS filtering, dashboards, document services, game services | Service integration, health checks, maintenance, and user-facing reliability |
| Operations | Git, scripted checks, monitoring, UPS-aware shutdown, change records | Repeatable updates, evidence-based verification, rollback, and incident response |

## Conceptual architecture

```mermaid
flowchart LR
    Internet((Internet)) --> Edge[Edge security and remote access]
    Edge --> Trusted[Trusted services zone]
    Edge --> Isolated[Isolated agent and workload zone]

    Trusted --> Compute[Virtualization and container compute]
    Isolated --> Compute

    Compute --> Storage[Central storage and backup]
    Compute --> AI[AI and automation services]
    Compute --> Apps[Self-hosted applications]

    AI --> Agents[Role-separated Hermes agents]
    Agents --> Channels[Approved messaging and work channels]
    Agents --> Tools[Scoped tools, files, and integrations]

    Operations[Monitoring, updates, recovery, and change control] -. governs .-> Edge
    Operations -. governs .-> Compute
    Operations -. governs .-> Storage
    Operations -. governs .-> Agents
```

The important part is not the number of applications. It is operating them as one system: deciding where they belong, limiting what they can reach, preserving state, updating without unnecessary downtime, and proving that recovery paths work.

## How I operate it

1. **Discover before changing.** Inventory the current state, dependencies, and failure domain.
2. **Protect state.** Take the appropriate configuration backup, snapshot, or rollback point.
3. **Change narrowly.** Update one layer or workload class at a time.
4. **Verify every hop.** Check the service, its dependencies, network path, storage path, and user-facing behavior.
5. **Record evidence.** Preserve what changed, what was tested, and what remains unresolved.
6. **Recover deliberately.** Use tested rollback and restore procedures instead of improvising under pressure.

The detail behind each step is in the docs below.

## Hermes agent environment

The lab includes multiple Hermes Agent instances with separate roles, identities, workspaces, communication routes, and permission boundaries. Depending on the role, an agent may use scheduled workflows, durable memory, approved file stores, research tools, local AI services, or narrowly scoped external integrations.

The public design principle:

```text
Untrusted input
  → bounded intake or specialist surface
  → explicit policy / approval boundary
  → narrowly scoped action
  → evidence returned to the owner
```

Privileged agents are not exposed as public chatbots, and public documentation does not include bot identities, channel identifiers, tokens, internal routes, or administrative URLs.

## What's in this repository

| Path | Contents |
| --- | --- |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | Layered capability view, boundary decisions, and the failure domains considered |
| [docs/PUBLIC-SERVICE-MAP.md](docs/PUBLIC-SERVICE-MAP.md) | Capability-level service map (deliberately not a live inventory) |
| [docs/OPERATIONS.md](docs/OPERATIONS.md) | Maintenance loop, verification layers, agent operations, and incident response |
| [SECURITY.md](SECURITY.md) | Disclosure rules and how to report something that should not be public |
| [scripts/privacy_scan.py](scripts/privacy_scan.py) | Scanner for secrets and infrastructure indicators |
| [tests/](tests/) | Unit tests for the scanner |
| [.github/workflows/verify.yml](.github/workflows/verify.yml) | CI: tests, privacy scan, and whitespace check on every push and pull request |

## What is intentionally absent

This repository does **not** contain:

- IP addresses, hostnames, domains, VLAN identifiers, ports, or VPN routes;
- exact physical topology or a complete list of running services;
- firewall, reverse-proxy, tunnel, or identity-provider configuration;
- credentials, tokens, account identifiers, recovery material, or private paths;
- live Compose files, environment files, backups, logs, or screenshots of administrative interfaces.

That omission is part of the design. A portfolio should demonstrate engineering judgment without making the real environment easier to target.

## Repository verification

Needs Python 3 and Git; there are no third-party packages to install.

```bash
python3 -m unittest discover -s tests -v
python3 scripts/privacy_scan.py
```

The scanner checks the working tree, the exact Git index, and reachable history for common secret and infrastructure indicators. Findings report category, file, and line only, never the matched value. Pass `--surface tree`, `--surface index`, or `--surface history` (repeatable) to limit the scan.

Operator-specific markers stay local:

```bash
cp local-patterns.txt.example local-patterns.txt   # gitignored; one literal per line
```

CI runs the same two commands plus `git diff --check` on every push and pull request.

## Related public projects

- [Presence Stack](https://github.com/whosebruce/presence-stack): privacy-first, agent-readable deployment harness for an owner-controlled digital presence.
- [Local-First AI Receptionist](https://github.com/whosebruce/local-first-ai-receptionist): tiered intake with explicit trust boundaries and offline security verification.
- [Hermes Discord Admin Pack](https://github.com/whosebruce/hermes-discord-admin-pack): sanitized setup and extension guide for Hermes Discord administration.

## License

MIT. See [LICENSE](LICENSE). Maintained by [@whosebruce](https://github.com/whosebruce).
