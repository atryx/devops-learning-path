<!-- GitAds-Verify: REPLACE_WITH_GITADS_CODE -->

# DevOps Learning Path (2026)

## GitAds Sponsored

[![Sponsored by GitAds](https://gitads.dev/v1/ad-serve?source=atryx/devops-learning-path@github)](https://gitads.dev/v1/ad-track?source=atryx/devops-learning-path@github)

A structured path from zero to production-ready DevOps engineer. Opinionated, practical, and focused on what companies actually hire for in 2026.

> **Star this repo** ⭐ and revisit as you progress. Each phase builds on the previous one.

---

## Table of Contents

- [How to Use This Roadmap](#how-to-use-this-roadmap)
- [Phase 1: Linux & Networking Foundations](#phase-1-linux--networking-foundations)
- [Phase 2: Version Control & Collaboration](#phase-2-version-control--collaboration)
- [Phase 3: Containers](#phase-3-containers)
- [Phase 4: CI/CD Pipelines](#phase-4-cicd-pipelines)
- [Phase 5: Cloud Platforms](#phase-5-cloud-platforms)
- [Phase 6: Infrastructure as Code](#phase-6-infrastructure-as-code)
- [Phase 7: Container Orchestration](#phase-7-container-orchestration)
- [Phase 8: Monitoring & Observability](#phase-8-monitoring--observability)
- [Phase 9: Security (DevSecOps)](#phase-9-security-devsecops)
- [Phase 10: Platform Engineering & SRE](#phase-10-platform-engineering--sre)
- [Hands-On Projects by Level](#hands-on-projects-by-level)
- [Certifications Worth Getting](#certifications-worth-getting)
- [Related Repos](#related-repos)

---

## How to Use This Roadmap

- **Go in order** — each phase assumes knowledge from previous ones
- **Build something** at each phase before moving on
- **Pick one cloud** (AWS, Azure, or GCP) and go deep
- Items marked with ⭐ are **highest priority** for 2026 job market
- Time estimates assume ~10-15 hrs/week of focused learning

---

## Phase 1: Linux & Networking Foundations

**Time:** 4-6 weeks

### Linux ⭐

You'll live in the terminal. Get comfortable.

- [ ] **File system** — navigation, permissions (`chmod`, `chown`), links
- [ ] **Users & groups** — creating, modifying, sudo
- [ ] **Process management** — `ps`, `top`, `htop`, `kill`, `systemctl`
- [ ] **Package managers** — `apt` (Debian/Ubuntu), `yum`/`dnf` (RHEL/Amazon)
- [ ] **Text processing** — `grep`, `awk`, `sed`, `cut`, `sort`, `uniq`
- [ ] **Shell scripting** — variables, loops, conditions, functions
- [ ] **File editors** — learn `vim` basics (or `nano`, but vim is everywhere on servers)
- [ ] **Cron jobs** — scheduling tasks
- [ ] **SSH** — key generation, config, tunneling, agent forwarding
- [ ] **Logs** — `journalctl`, `/var/log`, `tail -f`

> 📘 See also: [linux-one-liners](https://github.com/atryx/linux-one-liners)

### Networking

- [ ] **OSI model** — know layers 3 (Network), 4 (Transport), 7 (Application)
- [ ] **TCP vs UDP** — when and why
- [ ] **DNS** — how resolution works, A/AAAA/CNAME/MX records, TTL
- [ ] **HTTP/HTTPS** — methods, status codes, headers, TLS handshake
- [ ] **IP addressing** — IPv4, subnets, CIDR notation
- [ ] **Firewalls** — iptables/nftables basics, security groups
- [ ] **Tools** — `ping`, `traceroute`, `curl`, `dig`, `nslookup`, `netstat`/`ss`, `tcpdump`
- [ ] **Reverse proxy** — what it is, why every production app needs one

---

## Phase 2: Version Control & Collaboration

**Time:** 2-3 weeks

### Git ⭐

- [ ] `init`, `clone`, `add`, `commit`, `push`, `pull`, `fetch`
- [ ] Branching & merging
- [ ] Rebasing (interactive rebase is a superpower)
- [ ] Resolving merge conflicts
- [ ] `.gitignore` patterns
- [ ] Tags and releases
- [ ] Git hooks (pre-commit, pre-push)

> 📘 See also: [git-cheatsheet](https://github.com/atryx/git-cheatsheet)

### Branching Strategies

| Strategy | Best For |
|----------|----------|
| **Trunk-based** ⭐ | Teams with CI/CD, feature flags |
| **GitHub Flow** | Simple projects, small teams |
| **Git Flow** | Release-based projects, less frequent deploys |

### Collaboration

- [ ] Pull request workflows and code reviews
- [ ] Conventional commits (`feat:`, `fix:`, `chore:`)
- [ ] Branch protection rules
- [ ] CODEOWNERS file

---

## Phase 3: Containers

**Time:** 4-6 weeks

### Docker ⭐

- [ ] **What & why** — containers vs VMs, isolation, portability
- [ ] **Images** — Dockerfile, layers, caching, multi-stage builds
- [ ] **Containers** — run, stop, exec, logs, inspect
- [ ] **Volumes** — bind mounts vs named volumes, data persistence
- [ ] **Networks** — bridge, host, overlay; container-to-container comms
- [ ] **Docker Compose** — multi-service local environments
- [ ] **Best practices** — non-root user, `.dockerignore`, small images (Alpine/distroless)
- [ ] **Registries** — Docker Hub, GHCR, ECR, ACR

> 📘 See also: [docker-cheatsheet](https://github.com/atryx/docker-cheatsheet) | [docker-vs-podman](https://github.com/atryx/docker-vs-podman)

### Image Optimization

| Base Image | Size | Security | Use Case |
|-----------|------|----------|----------|
| `ubuntu:24.04` | ~77MB | More CVEs | When you need apt packages |
| `alpine:3.20` | ~7MB | Minimal | Default choice for most apps |
| `distroless` | ~2-20MB | Fewest CVEs | Production-only (no shell) |
| `scratch` | 0MB | None | Static Go binaries |

### Container Security

- [ ] Never run as root
- [ ] Scan images for CVEs (Trivy, Grype)
- [ ] Use specific tags, not `latest`
- [ ] Read-only root filesystem where possible
- [ ] Don't store secrets in images

---

## Phase 4: CI/CD Pipelines

**Time:** 4-6 weeks

### GitHub Actions ⭐ (Most Popular in 2026)

```yaml
# Minimal production pipeline
name: CI/CD
on:
  push:
    branches: [main]
  pull_request:

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm ci
      - run: npm test

  build:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: docker/build-push-action@v6
        with:
          push: ${{ github.ref == 'refs/heads/main' }}
          tags: ghcr.io/${{ github.repository }}:${{ github.sha }}

  deploy:
    needs: build
    if: github.ref == 'refs/heads/main'
    runs-on: ubuntu-latest
    environment: production
    steps:
      - run: echo "Deploy to production"
```

> 📘 See also: [production-ready-snippets](https://github.com/atryx/production-ready-snippets)

### CI/CD Concepts

- [ ] **Pipeline stages** — lint → test → build → scan → deploy
- [ ] **Artifacts** — build outputs passed between jobs
- [ ] **Caching** — speed up builds (npm cache, Docker layer cache)
- [ ] **Secrets management** — never hardcode, use encrypted secrets
- [ ] **Environments** — dev → staging → production with approvals
- [ ] **Blue/green deployments** — zero-downtime releases
- [ ] **Canary deployments** — roll out to a percentage of traffic
- [ ] **Rollbacks** — automated rollback on health check failure

### Other CI/CD Tools (Know They Exist)

| Tool | Best For |
|------|----------|
| **GitHub Actions** ⭐ | Default for GitHub-hosted projects |
| **GitLab CI** | GitLab-hosted projects, self-hosted |
| **Jenkins** | Legacy, self-hosted, enterprise |
| **ArgoCD** | GitOps for Kubernetes |
| **Tekton** | Cloud-native pipelines |

---

## Phase 5: Cloud Platforms

**Time:** 8-12 weeks (pick one cloud)

### Pick One ⭐

| Cloud | Market Share | Best For | Cert to Start |
|-------|-------------|----------|---------------|
| **AWS** ⭐ | ~32% | Everything, most job postings | SAA-C03 |
| **Azure** | ~23% | .NET shops, enterprise | AZ-104 |
| **GCP** | ~12% | Data/ML, Kubernetes | ACE |

### Core Services to Learn (Any Cloud)

| Category | AWS | Azure | GCP |
|----------|-----|-------|-----|
| **Compute** | EC2, ECS, Lambda | VMs, Container Apps, Functions | GCE, Cloud Run, Functions |
| **Storage** | S3 | Blob Storage | GCS |
| **Database** | RDS, DynamoDB | Azure SQL, Cosmos DB | Cloud SQL, Firestore |
| **Networking** | VPC, ALB, Route53 | VNet, App Gateway, DNS | VPC, Cloud LB, Cloud DNS |
| **IAM** | IAM, STS | Entra ID, RBAC | IAM, Workload Identity |
| **Containers** | ECR, ECS, EKS | ACR, ACA, AKS | AR, Cloud Run, GKE |
| **Messaging** | SQS, SNS, EventBridge | Service Bus, Event Grid | Pub/Sub |
| **Monitoring** | CloudWatch | Monitor, App Insights | Cloud Monitoring |

### Cloud Concepts

- [ ] Regions and availability zones
- [ ] VPCs, subnets, security groups
- [ ] Load balancers (ALB vs NLB vs Gateway)
- [ ] Auto-scaling (horizontal)
- [ ] Managed vs self-hosted services (prefer managed)
- [ ] Cost management and tagging
- [ ] IAM — least privilege principle
- [ ] Service accounts / workload identity (no long-lived keys)

---

## Phase 6: Infrastructure as Code

**Time:** 4-6 weeks

### Terraform ⭐

```hcl
# main.tf — Example: VPC + ECS cluster
terraform {
  required_providers {
    aws = { source = "hashicorp/aws", version = "~> 5.0" }
  }
  backend "s3" {
    bucket = "myapp-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}

resource "aws_vpc" "main" {
  cidr_block           = "10.0.0.0/16"
  enable_dns_hostnames = true
  tags = { Name = "myapp-vpc" }
}

resource "aws_ecs_cluster" "main" {
  name = "myapp-cluster"
  setting {
    name  = "containerInsights"
    value = "enabled"
  }
}
```

### IaC Concepts

- [ ] **State management** — remote state (S3, Azure Blob, GCS), locking
- [ ] **Modules** — reusable infrastructure components
- [ ] **Workspaces** — managing multiple environments
- [ ] **Plan → Apply** workflow — always review before applying
- [ ] **Drift detection** — when infrastructure changes outside Terraform
- [ ] **Import** — bringing existing resources under IaC management
- [ ] **Secrets** — never in `.tf` files (use Vault, SSM, env vars)

### Other IaC Tools

| Tool | When to Use |
|------|-------------|
| **Terraform** ⭐ | Multi-cloud, most popular |
| **OpenTofu** | Open-source Terraform fork |
| **Pulumi** | IaC in Python/TypeScript/Go/C# |
| **CloudFormation** | AWS-only, deep AWS integration |
| **Bicep** | Azure-only |
| **Crossplane** | Kubernetes-native IaC |

---

## Phase 7: Container Orchestration

**Time:** 8-12 weeks

### Kubernetes ⭐

**Important:** Don't start with K8s. You need containers, networking, Linux, and cloud first.

### Core Concepts

- [ ] **Pods** — smallest deployable unit
- [ ] **Deployments** — declarative pod management, rolling updates
- [ ] **Services** — ClusterIP, NodePort, LoadBalancer
- [ ] **Ingress** — HTTP routing, TLS termination
- [ ] **ConfigMaps & Secrets** — configuration management
- [ ] **Namespaces** — resource isolation
- [ ] **Storage** — PersistentVolumes, PersistentVolumeClaims, StorageClasses

### Operations

- [ ] **Health checks** — liveness, readiness, startup probes
- [ ] **Resource management** — requests and limits (CPU, memory)
- [ ] **HPA** — Horizontal Pod Autoscaler
- [ ] **RBAC** — role-based access control
- [ ] **Network policies** — pod-to-pod traffic control
- [ ] **Helm** — package manager for K8s
- [ ] **Kustomize** — template-free customization

### Managed Kubernetes

| Service | Cloud |
|---------|-------|
| **EKS** | AWS |
| **AKS** | Azure |
| **GKE** ⭐ | GCP (best K8s experience) |

**Don't self-host Kubernetes** unless you have a dedicated platform team. Use managed services.

### When NOT to Use Kubernetes

- [ ] You have fewer than 5-10 services
- [ ] Your team is < 5 engineers
- [ ] You don't have dedicated platform/infra people
- [ ] Simpler alternatives work (ECS, Cloud Run, Container Apps)

---

## Phase 8: Monitoring & Observability

**Time:** 4-6 weeks

### The Three Pillars

| Pillar | What | Tools |
|--------|------|-------|
| **Logs** | What happened (events) | Loki, ELK, CloudWatch Logs |
| **Metrics** | How much (numbers over time) | Prometheus + Grafana ⭐, Datadog |
| **Traces** | Where (request flow across services) | Jaeger, Tempo, OpenTelemetry ⭐ |

### Prometheus + Grafana ⭐

- [ ] Prometheus scraping and PromQL basics
- [ ] Grafana dashboards (USE method: Utilization, Saturation, Errors)
- [ ] Alerting rules and AlertManager
- [ ] Service discovery
- [ ] Recording rules (for expensive queries)

### OpenTelemetry ⭐

- [ ] Auto-instrumentation for your language
- [ ] Traces, metrics, and logs through a single SDK
- [ ] OTLP exporter to Jaeger/Tempo/Datadog
- [ ] Context propagation across services

### SRE Practices

- [ ] **SLIs** — Service Level Indicators (what you measure: latency, error rate, throughput)
- [ ] **SLOs** — Service Level Objectives (your target: 99.9% availability)
- [ ] **SLAs** — Service Level Agreements (contractual promise to customers)
- [ ] **Error budgets** — how much downtime is acceptable
- [ ] **Incident response** — runbooks, on-call, post-mortems
- [ ] **Blameless post-mortems** — focus on systems, not people

---

## Phase 9: Security (DevSecOps)

**Time:** 4-6 weeks

### Shift-Left Security

Integrate security into every pipeline stage:

```
Code → SAST → Build → Image Scan → Deploy → DAST → Monitor
       ↑                   ↑                   ↑
    Semgrep,          Trivy, Grype         OWASP ZAP
    CodeQL
```

### Security Checklist

- [ ] **Secrets management** — HashiCorp Vault, AWS Secrets Manager, Azure Key Vault
- [ ] **Image scanning** — Trivy, Grype, Snyk Container
- [ ] **Dependency scanning** — Dependabot, Renovate, Snyk
- [ ] **SAST** — CodeQL, Semgrep, SonarQube
- [ ] **DAST** — OWASP ZAP
- [ ] **Network policies** — restrict pod-to-pod traffic
- [ ] **mTLS** — encrypt service-to-service communication
- [ ] **RBAC** — least privilege, no shared accounts
- [ ] **Audit logging** — who did what, when
- [ ] **Compliance** — SOC2, HIPAA, GDPR awareness

---

## Phase 10: Platform Engineering & SRE

**Time:** Ongoing (senior level)

### Internal Developer Platform (IDP)

Build self-service infrastructure for your dev teams:

- [ ] **Service catalog** — Backstage, Port, Cortex
- [ ] **Golden paths** — pre-configured templates for new services
- [ ] **Self-service environments** — one-click staging/preview envs
- [ ] **Developer portal** — docs, APIs, runbooks in one place
- [ ] **Platform APIs** — abstract cloud complexity behind simple interfaces

### GitOps ⭐

```
Git repo (source of truth) → ArgoCD/Flux → Kubernetes cluster
```

- [ ] **ArgoCD** — declarative GitOps for Kubernetes
- [ ] Application definitions in Git
- [ ] Automated sync and drift detection
- [ ] Progressive delivery (Argo Rollouts)

### Chaos Engineering

- [ ] Litmus Chaos, Chaos Monkey
- [ ] Game days — planned failure injection
- [ ] Steady-state hypothesis testing
- [ ] Start small (kill one pod), scale up

---

## Hands-On Projects by Level

### Beginner
1. **Dockerize an app** — multi-stage build, compose, health checks
2. **CI pipeline** — GitHub Actions: lint → test → build → push image
3. **Deploy to cloud** — single EC2/VM with Nginx reverse proxy

### Intermediate
4. **IaC for a web app** — Terraform: VPC + RDS + ECS + ALB
5. **Monitoring stack** — Prometheus + Grafana + AlertManager on Docker Compose
6. **Zero-downtime deploy** — Blue/green with health checks and automated rollback

### Advanced
7. **Kubernetes cluster** — Deploy a microservice app on EKS/AKS/GKE with Helm
8. **GitOps pipeline** — ArgoCD syncing from Git to K8s
9. **Full observability** — OpenTelemetry traces + Prometheus metrics + Loki logs

### Senior / Platform
10. **Internal Developer Platform** — Backstage catalog + golden path templates
11. **Multi-region deployment** — Active-active with global load balancing
12. **Chaos engineering** — Inject failures, verify SLOs hold

---

## Certifications Worth Getting

| Cert | Cloud | Level | Value |
|------|-------|-------|-------|
| **CKA** (Certified Kubernetes Admin) | Any | Intermediate | ⭐⭐⭐ Very high |
| **AWS SAA-C03** | AWS | Associate | ⭐⭐⭐ Great starting point |
| **Terraform Associate** | Multi | Associate | ⭐⭐ Good signal |
| **AZ-104** | Azure | Associate | ⭐⭐ Strong in enterprise |
| **CKS** (K8s Security) | Any | Advanced | ⭐⭐ Niche but valuable |
| **AWS DevOps Pro** | AWS | Professional | ⭐⭐ Advanced, impressive |

**Order:** AWS SAA or AZ-104 → Terraform → CKA → specialize

---

## Related Repos

| Repo | What's Inside |
|------|---------------|
| [backend-developer-roadmap-2026](https://github.com/atryx/backend-developer-roadmap-2026) | Backend developer learning path |
| [ai-engineer-roadmap-2026](https://github.com/atryx/ai-engineer-roadmap-2026) | AI/ML engineer roadmap |
| [mlops-engineering-roadmap-2026](https://github.com/atryx/mlops-engineering-roadmap-2026) | MLOps engineering path |
| [spring-boot-advanced-roadmap](https://github.com/atryx/spring-boot-advanced-roadmap) | Advanced Spring Boot topics |
| [docker-cheatsheet](https://github.com/atryx/docker-cheatsheet) | Docker commands quick reference |
| [git-cheatsheet](https://github.com/atryx/git-cheatsheet) | Git commands cheat sheet |
| [linux-one-liners](https://github.com/atryx/linux-one-liners) | Linux one-liners |
| [docker-vs-podman](https://github.com/atryx/docker-vs-podman) | Docker vs Podman compared |
| [production-ready-snippets](https://github.com/atryx/production-ready-snippets) | Production-ready config snippets |
| [awesome-dev-errors](https://github.com/atryx/awesome-dev-errors) | Real error messages + fixes |

---

## Contributing

Missing a tool? Better resource? Outdated recommendation? PRs welcome — see [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
