# Oracle Cluster Deployment

GitOps-managed manifests for the Oracle Harvester cluster.

## 🧱 Structure
- apps/ — Application charts (Traefik, cert-manager)
- secrets/ — SOPS-encrypted secret values
- kustomization.yaml — Declares resources to apply

## 🛠️ Decryption
```bash
sops -d clusters/harvester/oracle/secrets/cloudflare-api.yaml

## 🧪 Test Manifests
```bash
kustomize build clusters/harvester/oracle
