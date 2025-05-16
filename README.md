# Personal Infrastructure Deployments

This repository contains a GitOps-managed Kubernetes configuration for multiple Harvester clusters, using:

- SOPS + Age for secret management
- Helm for application lifecycle
- kustomize for overlay composition
- GitHub Actions for CI version checks

## 🌎 Environments

- **Homelab**: On-prem Harvester cluster
- **Oracle**: Cloud-based Harvester cluster (Oracle Cloud)

## 🗂️ Repository Structure

This repository is organized for managing infrastructure deployments using GitOps practices. Below is an overview of the directory layout:

```
personal-infra-deployments/
├── .github/
│   └── workflows/
│       └── validate-kustomize-and-sops.yaml       # CI for validating manifests and secrets
├── clusters/
│   └── harvester/
│       ├── homelab/
│       │   ├── apps/
│       │   │   ├── cert-manager/
│       │   │   │   └── resources/                 # Cert-manager CRs
│       │   │   └── traefik/
│       │   │       └── resources/                 # Traefik configuration
│       │   └── secrets/                           # SOPS-encrypted secrets for homelab
│       └── oracle/
│           ├── apps/
│           │   ├── cert-manager/
│           │   │   └── resources/
│           │   └── traefik/
│           │       └── resources/
│           └── secrets/                           # SOPS-encrypted secrets for oracle
├── .gitattributes
├── .gitignore
├── .sops.yaml                                     # SOPS config for age-encrypted secrets
├── LICENSE
└── README.md
```

- **clusters/**: Contains environment-specific Kustomize overlays for deploying on Harvester nodes.
- **.sops.yaml**: Defines file patterns and encryption keys for managing secrets with Mozilla SOPS.
- **.github/workflows/**: GitHub Actions workflows, including automated validation for Kustomize and SOPS.

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
