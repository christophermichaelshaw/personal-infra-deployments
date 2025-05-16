# Personal Infrastructure Deployments

This repository contains a GitOps-managed Kubernetes configuration for multiple Harvester clusters, using:

- SOPS + Age for secret management
- Helm for application lifecycle
- kustomize for overlay composition
- GitHub Actions for CI version checks

## 🌎 Environments

- **Homelab**: On-prem Harvester cluster
- **Oracle**: Cloud-based Harvester cluster (Oracle Cloud)

## 🗂️ Folder Structure

clusters/
└── harvester/
├── base/ # Shared common resources
├── homelab/ # Homelab overlay
└── oracle/ # Oracle overlay

## 🔐 Secrets Management

Secrets (e.g., Cloudflare API token) are encrypted with Age + SOPS and committed safely to Git.


### Encrypt
```bash
sops -e -i clusters/harvester/homelab/secrets/cloudflare-api.yaml
```

### Decrypt
```bash
sops -d clusters/harvester/homelab/secrets/cloudflare-api.yaml
```

## 🛠️ Tooling
- SOPS
- Age
- kustomize
- Helm
- GitHub Actions — checks for Helm chart version drift

## 🚀 GitOps Workflow

### Render manifests
```bash
kustomize build clusters/harvester/homelab
```

### Apply to cluster
```bash
kubectl apply -k clusters/harvester/homelab
```
