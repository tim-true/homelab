# homelab

Docker Compose services running on two Raspberry Pi 4 (4GB) nodes.

## Infrastructure

| Component | Details |
|---|---|
| node0 | Raspberry Pi 4 (4GB) — primary services host |
| node1 | Raspberry Pi 4 (4GB) — agents, secondary DNS |
| Domain | Custom domain (DNS via Cloudflare) |
| NAS | QNAP TS-453Be |

## Services

### node0

| Subdomain | Service |
|---|---|
| `npm.*` | Nginx Proxy Manager (admin) |
| `portainer.*` | Portainer (server) |
| `homepage.*` | Homepage dashboard |
| `grafana.*` | Grafana |
| `prometheus.*` | Prometheus |
| `pihole0.*` | Pi-hole (primary) |
| `n8n.*` | n8n |
| `cockpit.*` | Cockpit |
| `ntfy.*` | ntfy |
| `dockge.*` | Dockge |
| `dozzle.*` | Dozzle |
| `uptime.*` | Uptime Kuma |
| `cyberchef.*` | CyberChef |
| `ittools.*` | IT-Tools |
| — | Prometheus node-exporter |
| — | Tailscale |

### node1

| Subdomain | Service |
|---|---|
| — | Dockge agent |
| — | Dozzle agent |
| — | Portainer agent |
| `pihole1.*` | Pi-hole (secondary) |
| — | Prometheus node-exporter |
| — | Tailscale |

## Deployment

SSH into the node, then `cd ~/homelab/<service>` and run:

```bash
docker compose up -d
```

To update a service:

```bash
docker compose pull && docker compose up -d
```

## Next Steps
- Customize Cockpit. 
- Complete Heimdall configuration and test. 
- Finish and test OpenWebUI on a beefier piece of hardware. 
- Setup actual notification rules for ntfy. 
- Setup grafana for Qnap nas. 
- Configure docker on Qnap and add environment to portainer
- Build out nextcloud config, running on qnap.
