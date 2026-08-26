# Public Service Map

This is a capability-oriented view of the environment. It is intentionally **not** an authoritative inventory of live hosts, endpoints, or exposure.

## Network foundation

- OPNsense firewall and routing
- Managed Ethernet switching
- Mesh wireless access
- Segmented trusted and isolated workload zones
- Local DNS filtering
- Tailscale-based private remote access
- Cloudflare and Caddy for selected DNS, TLS, and reverse-proxy workflows

## Compute and platform

- Proxmox VE virtualization
- Linux virtual machines
- Docker and Docker Compose workloads
- Hardware and GPU passthrough
- Dedicated roles for storage, AI acceleration, agents, general services, and isolated workloads
- UPS monitoring and graceful-shutdown planning

## Storage and state

- TrueNAS SCALE
- NAS-backed application and media data
- SMB file services
- Snapshots and rollback points
- Separate backup and restore procedures
- Scoped application permissions and agent access

## AI, agents, and research

- Hermes Agent gateways and specialist profiles
- Hosted-model orchestration with explicit fallbacks
- Ollama and Open WebUI for selected local-model workloads
- SearXNG and Firecrawl for research and page extraction
- Scheduled workflows, durable memory, and human-readable knowledge stores
- Role-separated communication and approval paths

## Automation and observability

- n8n and scheduled agent workflows
- Service health checks and availability monitoring
- Update discovery and staged maintenance
- Change records, verification receipts, and rollback notes
- Dashboards for selected infrastructure, agent, and business workflows

## User-facing service classes

- Home automation
- Media streaming and media-management tools
- Document and file services
- Password and credential-management services
- DNS filtering
- Collaborative whiteboarding and dashboards
- Game-server management
- Private business and operations tools

## Why the map stops here

Publishing every product name, version, host, route, and administrative interface would turn a portfolio into reconnaissance material. The private operational inventory remains separate from this public capability map.
