# personal-infra-deployments

Infrastructure-as-Code for managing a hybrid personal infrastructure platform using GitOps, Kubernetes, and automation tooling.

This repository manages:

- 🏠 **HomeLab Infrastructure** using Harvester + K3s
- ☁️ **Oracle Cloud Free Tier (OCI)** running K3s
- ⚙️ **Ansible-managed VMs** for specialized workloads (e.g., Fedora Server, Wazuh, LibreNMS)
- 📦 **GitOps deployments** via [Rancher Fleet](https://fleet.rancher.io/)
- 🔐 **SOPS + Age** secrets management with YubiKey and offline key support
- 🌐 **Traefik + Cert-Manager** for ingress, TLS, and Cloudflare DNS-01 automation
- 🛡️ **Authentik** for centralized SSO across clusters and services

## ✨ GitOps Architecture

- All workloads are declared in Kubernetes manifests (Helm/Kustomize)
- Managed via **Rancher Fleet**, with separate cluster paths for:
  - `clusters/homelab/`
  - `clusters/oracle/`
- Secrets are stored encrypted in Git using **SOPS** and decrypted at deployment time

## 📁 Repository Structure

```plaintext
.github/workflows/        → GitHub Actions CI/CD for validation/deployment
ansible/                  → Ansible roles, inventory, playbooks for VM lifecycle
apps/                     → Helm values, app-specific overlays (e.g., Traefik, Authentik)
clusters/
  ├── homelab/            → Fleet deployment path for HomeLab cluster
  └── oracle/             → Fleet deployment path for OCI cluster
secrets/                  → SOPS-encrypted Kubernetes Secret manifests
sops.yaml                 → SOPS config for encrypted keys and rules
