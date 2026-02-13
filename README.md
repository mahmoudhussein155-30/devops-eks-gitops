# GitOps Repository

This repository contains Kubernetes manifests for all applications and platform services managed by Argo CD.

## Structure

```
├── applications/          # Application deployments
│   ├── dev/              # Development environment
│   ├── staging/          # Staging environment
│   └── prod/             # Production environment
├── platform/             # Platform services (Nexus, SonarQube, etc.)
│   ├── dev/
│   ├── staging/
│   └── prod/
└── manifests/            # Raw Kubernetes manifests
    ├── dev/
    ├── staging/
    └── prod/
```

## Deployment Workflow

1. **CI Pipeline** builds and pushes Docker images to Nexus
2. **CI Pipeline** updates image tags in this repository
3. **Argo CD** detects changes and syncs to Kubernetes
4. **Automated deployment** to dev/staging
5. **Manual approval** required for production

## Adding a New Application

1. Create application directory under `applications/<env>/`
2. Add Helm values or Kubernetes manifests
3. Create Argo CD Application manifest
4. Commit and push to trigger deployment

## Best Practices

- Never commit secrets - use External Secrets Operator
- Always test in dev before promoting to staging/prod
- Use semantic versioning for image tags
- Document all configuration changes in commit messages
