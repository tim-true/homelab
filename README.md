# homelab

Docker Compose services running on a Raspberry Pi 4 (4GB).

## Infrastructure

| Component | Details |
|---|---|
| Host | Raspberry Pi 4 (4GB) |
| Domain | Custom domain (DNS via Cloudflare) |
| NAS | QNAP TS-453Be |

## Network

Access is **Tailscale-only**. A wildcard DNS record points to the Tailscale IP — the domain is unreachable without a Tailscale connection.

```
Client (Tailscale)
      │
      ▼
 *.domain
      │
      ▼
Nginx Proxy Manager (80/443)
  ├── SSL wildcard cert via Let's Encrypt (Cloudflare DNS challenge)
  └── Reverse proxies to each service on the Pi
```

## Services

| Subdomain | Service | Host Port |
|---|---|---|
| `npm.*` | Nginx Proxy Manager (admin) | 81 |
| `portainer.*` | Portainer | 9443 |
| `homepage.*` | Homepage dashboard | 3030 |
| `grafana.*` | Grafana | 3000 |
| `prometheus.*` | Prometheus | 9090 |
| `pihole.*` | Pi-hole | 8180 |
| `n8n.*` | n8n | 5678 |
| `nextcloud.*` | Nextcloud | 8080 |
| `cockpit.*` | Cockpit (host network) | 9091 |
| `ntfy.*` | ntfy | — |
| `qnap.*` | QNAP web UI | — |
| `plex.*` | Plex (QNAP) | — |
| — | Prometheus node-exporter | 9100 |
| — | SNMP exporter | 9116 |

## Repo layout

Each service lives in its own directory with a `docker-compose.yml` and any config files alongside it.

```
homelab/
├── cockpit/
├── grafana/
├── heimdall/
├── homepage/
├── n8n/
├── nextcloud/
├── nginx-proxy-manager/
├── ntfy/
├── pihole/
├── portainer/
├── prometheus/
├── snmp-exporter/
└── tailscale/
```

## Deployment

SSH into the Pi, then `cd ~/homelab/<service>` and run:

```bash
docker compose up -d
```

To update a service:

```bash
docker compose pull && docker compose up -d
```

## Gotchas

- **Pi-hole** is on host port `8180` (not 80) so NPM can own 80/443.
- **Portainer** proxy host requires `proxy_ssl_verify off;` in NPM's Advanced tab.
- **Pi-hole** proxy host needs a redirect in NPM's Advanced tab: `location = / { return 301 /admin/; }`
- **OpenWebUI** OOMs the Pi when other services are running — not deployed.
- **Heimdall** is not fully configured and working. 

## Next Steps
- Customize Cockpit. 
- Complete Heimdall configuration and test. 
- Finish and test OpenWebUI on a beefier piece of hardware. 
- Setup actual notification rules for ntfy. 
- Setup grafana for Qnap nas. 
- Configure docker on Qnap and add environment to portainer
- Build out nextcloud config, running on qnap. 

