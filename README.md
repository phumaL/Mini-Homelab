# Home Lab Server

Final milestone (PMF, W13) — Data Communications / Linux System Administration @ UJ (IT28X97).

A self-hosted home server stack running in a VirtualBox Ubuntu VM. All services are Docker containers routed through Traefik with wildcard DNS from dnsmasq.

## Stack

| Service | URL | Version |
|---|---|---|
| Traefik + dnsmasq | http://traefik.local | v2.11 |
| Gitea | http://gitea.local | 1.22.3 |
| Immich | http://immich.local | v1.117.0 |
| Stirling PDF | http://stirling.local | 0.38.1 |
| DokuWiki | http://wiki.local | 2024-02-06a |

## Quick Start

```bash
# 1. Create the shared proxy network (once only)
docker network create proxy

# 2. Copy and fill in secrets
cp traefik/.env.example traefik/.env
cp gitea/.env.example   gitea/.env
cp immich/.env.example  immich/.env

# 3. Start services in order
docker compose -f traefik/docker-compose.yml up -d
docker compose -f gitea/docker-compose.yml up -d
docker compose -f immich/docker-compose.yml up -d
docker compose -f stirling-pdf/docker-compose.yml up -d
docker compose -f wiki/docker-compose.yml up -d
```

## VM Setup

- VirtualBox Ubuntu Server VM
- Host-only adapter at `192.168.56.3`
- Host DNS must forward `*.local` to `192.168.56.3:53`

Full setup documentation at `http://wiki.local` once running.

## Repository Layout

```
final-data-comms/
├── traefik/          # Reverse proxy + dnsmasq
├── gitea/            # Self-hosted Git + Postgres
├── immich/           # Photo management
├── stirling-pdf/     # PDF tools
└── wiki/             # DokuWiki + page content
    └── data/data/pages/
```
