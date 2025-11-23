# KubeRule Configuration Repository

KubeRule policies and Kubernetes manifests for GitOps-based security and compliance scanning.

## Structure

```
demo-repo/
├── kuberule/
│   └── policies/
│       ├── cve.yaml
│       ├── drift.yaml
│       └── observability.yaml
└── manifests/
    └── demo-apps/
        └── demo-workloads.yaml
```

## Configuration

### Policies

- **cve.yaml**: CVE scanning thresholds and settings
- **drift.yaml**: Drift detection configuration and repository settings
- **observability.yaml**: Compliance and metadata requirements

### Manifests

Kubernetes manifests for drift detection comparison.

## Setup

1. Update `kuberule/policies/drift.yaml` with your repository URL
2. Configure KubeRule deployment:

```bash
kubectl -n kuberule-system set env deployment/kuberule \
  KUBERULE_GIT_REPO="https://github.com/YOUR_USERNAME/demo-repo" \
  KUBERULE_GIT_BRANCH="main" \
  KUBERULE_GIT_PATH=""

kubectl -n kuberule-system rollout restart deployment/kuberule
```

3. KubeRule will automatically pull policies on each scan cycle

## Private Repositories

For private repositories, create a GitHub token secret:

```bash
kubectl -n kuberule-system create secret generic kuberule-git-auth \
  --from-literal=token="ghp_YOUR_TOKEN"
```
