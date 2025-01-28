# Flux Configuration Repository

## Overview

This repository contains the Flux configuration files for our Kubernetes infrastructure. Flux is used for GitOps-style continuous delivery, automatically synchronizing our Kubernetes cluster with the configurations defined in this repository.

## Structure

├── clusters/
│ └── production/
│ ├── flux-system/
│ └── apps/
├── infrastructure/
├── apps/
└── README.md


- `clusters/`: Contains cluster-specific configurations
  - `production/`: Production cluster configurations
    - `flux-system/`: Flux system components
    - `apps/`: Application deployments for the production cluster
- `infrastructure/`: Shared infrastructure components (e.g., ingress controllers, monitoring tools)
- `apps/`: Application configurations (shared across clusters if applicable)

## Usage

1. Ensure you have Flux CLI installed:

flux check --pre


2. Bootstrap Flux on your cluster:

flux bootstrap github
--owner=<your-github-username>
--repository=flux-config
--branch=main
--path=./clusters/production


3. Flux will automatically synchronize your cluster with the configurations in this repository.

## Adding New Applications

1. Create a new directory under `apps/` for your application.
2. Add your Kubernetes manifests (deployments, services, etc.) to this directory.
3. Create a `kustomization.yaml` file in the application directory.
4. Reference your application in the appropriate cluster's `kustomization.yaml` file.

## Monitoring

- Access the Flux UI to monitor reconciliation status:

kubectl port-forward svc/flux-ui -n flux-system 8080:80

Then open `http://localhost:8080` in your browser.

## Troubleshooting

- Check Flux logs:

flux logs --all-namespaces


- Manually trigger a reconciliation:

flux reconcile source git flux-system


## Contributing

1. Create a new branch for your changes.
2. Make your changes and commit them.
3. Push your branch and create a pull request.
4. After review and approval, merge the pull request.

## Security

Ensure that sensitive information (secrets, credentials) are not committed to this repository. Use Kubernetes Secrets or a secrets management solution integrated with Flux.

## License

[Specify your license here]
