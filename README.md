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
- Setup actual notification rules for ntfy. 
- Bring monitoring back up on nas for Grafana. 
- Configure docker on Qnap and add environment to portainer
- Determine if possible to fix Nextcloud heavy io usage - too much on usb storage, might need to run on other hardware. 
- Fix speedtest-tracker compose
- Bring OpenWebUI up on node1 as well as freellmapi project

