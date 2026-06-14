# vault-eso-demo
# Vault + External Secrets Operator — Demo

## Description
Démonstration d'une gestion des secrets Kubernetes GitOps-native avec HashiCorp Vault et External Secrets Operator (ESO).

## Architecture
## Stack technique
- Kind v0.32 — cluster Kubernetes local
- HashiCorp Vault v1.15 — stockage des secrets
- External Secrets Operator v0.9 — synchronisation
- Helm v4.2 — déploiement des composants

## Installation

### 1. Créer le cluster
```bash
kind create cluster --name vault-demo
```

### 2. Installer Vault
```bash
helm repo add hashicorp https://helm.releases.hashicorp.com
helm install vault hashicorp/vault \
  --set "server.dev.enabled=true" \
  --set "server.dev.devRootToken=root" \
  --namespace vault --create-namespace
```

### 3. Installer ESO
```bash
helm repo add external-secrets https://charts.external-secrets.io
helm install external-secrets external-secrets/external-secrets \
  --namespace external-secrets --create-namespace
```

### 4. Appliquer les manifests
```bash
kubectl apply -f k8s/secretstore.yaml
kubectl apply -f k8s/externalsecret.yaml
```

## Résultat
- Aucun secret dans Git
- Synchronisation automatique toutes les 1 minute
- Rotation des secrets sans downtime