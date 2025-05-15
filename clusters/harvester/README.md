## 📄 `/clusters/harvester/README.md` (Harvester-Specific)

```md
# Harvester GitOps Configuration

This directory manages shared Kubernetes configuration and app deployments across Harvester-based clusters.

## 🧱 Components

- `base/` — Shared kustomize components for all Harvester clusters
- `homelab/` — Homelab-specific overlays and secrets
- `oracle/` — Oracle Cloud-specific overlays and secrets

## 🧩 Applications

- **cert-manager**: Issues DNS01 certificates via Cloudflare
- **traefik**: Provides ingress with Let's Encrypt support

## 🔐 Secrets

- Secrets live under `secrets/` per environment and are encrypted with SOPS.
- All `.yaml` secrets are excluded from plain text via `.gitattributes` and `.sops.yaml`.
