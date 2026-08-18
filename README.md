# Infra

This repository is a "meta" repo that manages multiple repos at once.
Specifically this repo manages physical and logical infrastructure for Levi Zitting, SGF Devs, and Open SGF.
Meta repo management is handled by [mani](https://manicli.com/) which is a tool that makes it easy to run commands across repos.

## Sub-repositories

### LZ

- [`lz/infra-aws-core`](https://github.com/glitchedmob/infra-aws-core): Provisions LZ's shared AWS foundation, including Terraform/OpenTofu state backend, GitHub OIDC CI access, and baseline IAM Identity Center access controls.
- [`lz/infra-dns`](https://github.com/glitchedmob/infra-dns): Manages DNS records for the `levizitting.com` domain as code with OpenTofu and CI plan/apply workflows.
- [`lz/infra-gha`](https://github.com/glitchedmob/infra-gha): Provides reusable GitHub Actions workflows and composite actions used by infra repos for Terraform/OpenTofu and Ansible automation.
- [`lz/infra-app-config`](https://github.com/glitchedmob/infra-app-config): Manages post-bootstrap configuration for LZ edge-hosted applications, currently Headscale users, ACL policy, and pre-auth key lifecycle with credentials stored in AWS SSM Parameter Store.
- [`lz/infra-k8s-apps`](https://github.com/glitchedmob/infra-k8s-apps): Holds the Kubernetes manifests for base infrastructure and applications deployed to the LZ k3s cluster.
- [`lz/infra-on-prem`](https://github.com/glitchedmob/infra-on-prem): Operates on-prem networking and virtualization hosts (MikroTik + Proxmox) with OpenTofu plus Ansible host lifecycle automation.
- [`lz/infra-public-edge`](https://github.com/glitchedmob/infra-public-edge): Provisions and operates the LZ public edge node, including the Kubernetes resources for edge routing and edge-hosted services.
- [`lz/infra-shared`](https://github.com/glitchedmob/infra-shared): Hosts reusable OpenTofu modules (for example Proxmox VM and SSH key/SSM patterns) consumed by other infra repositories.
- [`lz/infra-vm-workloads`](https://github.com/glitchedmob/infra-vm-workloads): Provisions LZ workload VMs on Proxmox and performs K3s + Flux bootstrap and configuration through Ansible.

### SGF Devs

- [`sgfdevs/infra-app-config`](https://github.com/sgfdevs/infra-app-config): Manages post-bootstrap OpenBao OIDC and backup authentication configuration.
- [`sgfdevs/infra-aws-core`](https://github.com/sgfdevs/infra-aws-core): Provisions SGF Devs shared AWS core primitives such as remote state backend, CI OIDC IAM role, and account access baseline.
- [`sgfdevs/infra-dns`](https://github.com/sgfdevs/infra-dns): Manages Cloudflare DNS records for the `sgf.dev` zone as code with OpenTofu and CI validation/apply flows.
- [`sgfdevs/infra-gh`](https://github.com/sgfdevs/infra-gh): Manages SGF Devs GitHub organization teams, repository access, and repository governance as code with OpenTofu.
- [`sgfdevs/infra-k8s-apps`](https://github.com/sgfdevs/infra-k8s-apps): Holds the Kubernetes manifests for base infrastructure and applications deployed to the SGF Devs k3s cluster.
- [`sgfdevs/infra-vm-workloads`](https://github.com/sgfdevs/infra-vm-workloads): Provisions SGF Devs workload VMs on Proxmox and performs K3s + Flux bootstrap and configuration through Ansible.

### Open SGF

- [`opensgf/infra-aws-core`](https://github.com/Open-SGF/infra-aws-core): Provisions Open SGF shared AWS core primitives such as the remote state backend, CI OIDC IAM role, and account access baseline.
- [`opensgf/infra-dns`](https://github.com/Open-SGF/infra-dns): Manages Cloudflare DNS records for the `opensgf.org` zone as code with OpenTofu and CI validation/apply flows.
- [`opensgf/infra-gh`](https://github.com/Open-SGF/infra-gh): Manages OpenSGF GitHub organization teams, repository access, and repository governance as code with OpenTofu.

## Common meta-repo commands

```bash
mani check
mani list projects
mani run git-status --target lz-tf
mani run git-fetch --target ansible
mani exec --target k8s 'make help'
```
