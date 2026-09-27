Here’s the 20% of DevOps knowledge that delivers 80% of the daily value - focused on what you’ll actually touch every week rather than the full landscape.

## 1. **The Core Loop: Source → Build → Deploy**
**Git fundamentals** (not just `commit`/`push`):
- Branching strategies (trunk-based or GitFlow—know when to use which)
- Pull requests as quality gates, not just code review
- **Why this matters**: Every other DevOps process hangs off this. If your Git hygiene is bad, everything downstream suffers.

**Containerization with Docker**:
- Writing a *good* Dockerfile (multi-stage builds, layer caching, non-root users)
- Docker Compose for local development parity
- **80% rule**: You don’t need Kubernetes expertise yet. You need to know how to containerize an app reliably and debug it when it breaks.

## 2. **CI/CD: The Automation Backbone**
**One pipeline tool deeply** (GitHub Actions, GitLab CI, or Jenkins—pick your ecosystem’s default):
- Build → Test → Deploy workflows
- Environment variables and secrets management
- Caching dependencies (this is the difference between 3-minute and 30-minute builds)
- **Daily reality**: You’ll spend more time debugging YAML indentation than writing complex deployment logic.

**Infrastructure as Code (IaC) - The 80% version**:
- **Terraform** for cloud resources (or CloudFormation if you’re AWS-locked)
- You don’t need to know every provider—just how to create, modify, and destroy compute, networking, and databases safely
- **State management** (remote state, locking) is the part that actually matters in teams

## 3. **Cloud Fundamentals (Pick One, Know It Well)**
**AWS, Azure, or GCP**—doesn’t matter which, but know these three services intimately:
- **Compute**: EC2/VMs or managed containers (ECS/App Service/Cloud Run)
- **Networking**: VPCs, security groups/firewalls, load balancers
- **Identity**: IAM roles and policies (most security incidents happen here)
- **80% rule**: You don’t need 200 services. You need to debug why an app can’t reach a database (90% of your time).

## 4. **Observability: Knowing When Things Break**
**The three pillars (practical usage)**:
- **Logs**: Structured logging (JSON), log aggregation (CloudWatch/ELK/Stackdriver)
- **Metrics**: CPU, memory, disk, plus RED method (Rate, Errors, Duration) for services
- **Alerting**: Alert on symptoms (user-facing errors), not causes (disk space)—unless it’s predictive
- **Reality check**: You’ll spend more time reading logs than writing code. Learn `grep`, `jq`, and your cloud’s log query language.

## 5. **Configuration Management (The Modern 80%)**
**Ansible or equivalent** (or even just cloud-init scripts):
- You don’t need complex Puppet/Chef architectures anymore
- Know how to idempotently install packages, manage files, and restart services
- **Modern twist**: Often replaced by "immutable infrastructure" (bake config into containers), but you still need it for the "golden image" baseline.

## 6. **The "Glue" Skills (Where Juniors Struggle)**
**Linux/Unix fluency**:
- `ssh`, `systemd` (or at least reading logs via `journalctl`), file permissions, `curl` for debugging APIs
- **Bash scripting**: Not for complex apps, but for gluing steps together in pipelines

**Networking basics**:
- DNS (A records, CNAMEs, TTLs), TCP vs UDP, HTTP status codes, TLS certificates
- **80% of outages** are DNS, certificates, or security group changes.

## 7. **Security & Secrets (The Non-Negotiable 20%)**
- **Never** hardcode secrets; use vaults (AWS Secrets Manager, HashiCorp Vault, or CI/CD secret stores)
- Principle of least privilege (IAM roles over access keys)
- Dependency scanning in CI (Dependabot/Snyk)—set it and forget it

## What to *Skip* (For Now)
- **Kubernetes**: Unless you’re specifically hired for it, learn it after you’ve mastered containers and CI/CD. It’s a complexity multiplier.
- **Service Mesh (Istio/Linkerd)**: Solves problems you don’t have yet.
- **Multi-cloud**: Master one cloud first. The concepts transfer.
- **GitOps (ArgoCD/Flux)**: Evolved CI/CD; learn basic CI/CD first.

## The 80% Workflow You’ll Actually Live In
1. **Morning**: Check overnight alerts (CloudWatch/Grafana), scan logs for errors
2. **Midday**: Review PR, merge to main, watch pipeline deploy to staging
3. **Afternoon**: Debug why the staging deploy can’t reach the database (security group rule)
4. **Evening**: Update Terraform to add a new environment variable, plan/apply carefully

**Your force multiplier**: Learn to **read error messages** and **check logs first** before changing code. 80% of "DevOps issues" are configuration, not code.

If you master just the **Git → Docker → CI/CD → Cloud (one provider) → Logs** chain, you can handle the daily demands of most DevOps roles. The rest is optimization.
