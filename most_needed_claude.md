## DevOps core you should actually know well:

## 1. Version Control (Git)
Non-negotiable foundation. Branching strategies, merge vs rebase, resolving conflicts, PR workflows. Everything else builds on this.

## 2. Linux & Command Line
Most infra runs on Linux. File permissions, process management, systemd, networking basics (ports, DNS, firewalls), shell scripting (bash).

## 3. CI/CD
- **Concepts**: build → test → deploy pipeline
- **Tools**: GitHub Actions, GitLab CI, Jenkins (pick one deeply, understand the pattern generally)
- Know how to write a pipeline config, manage secrets, and set up automated testing/deployment gates.

## 4. Containers (Docker)
Writing efficient Dockerfiles, image layers, multi-stage builds, docker-compose for local dev. This is the packaging standard now.

## 5. Container Orchestration (Kubernetes)
Even if you don't master it, understand: pods, deployments, services, ingress, ConfigMaps/Secrets, and how scaling/self-healing works. This is where a lot of DevOps roles live.

## 6. Infrastructure as Code (IaC)
Terraform is the industry default (cloud-agnostic). Know how to define, plan, and apply infrastructure changes instead of clicking around cloud consoles.

## 7. Cloud Platforms
Pick one deeply (AWS, GCP, or Azure) — compute, storage, networking (VPCs), IAM. AWS has the most market share if you're choosing.

## 8. Monitoring & Observability
- **Metrics**: Prometheus + Grafana
- **Logs**: ELK/Loki stack
- Understand the difference between monitoring (is it broken?) and observability (why is it broken?).

## 9. Networking Fundamentals
DNS, load balancing, reverse proxies (Nginx), TLS/SSL, how HTTP requests actually flow through your infra.

## 10. Security basics
Secrets management (Vault, cloud-native secret stores), least-privilege IAM, basic vulnerability scanning in pipelines.

---

**If I had to rank priority for someone starting out**: Git → Linux/bash → Docker → CI/CD → one cloud provider → Kubernetes → Terraform → monitoring.

## Suggested learning path/order with a rough timeline

Here's a realistic path assuming consistent part-time study (10-15 hrs/week). Adjust down if you're full-time on this.

## Phase 1: Foundations (Weeks 1–4)
**Goal: comfortable in a terminal, comfortable with Git**
- Linux basics: filesystem, permissions, processes, package managers, systemd
- Bash scripting: variables, loops, conditionals, piping/grep/awk/sed
- Git: branching, merging, rebasing, resolving conflicts, PR workflow
- Networking basics: IP/DNS/ports/HTTP vs HTTPS

*Milestone: write a bash script that automates something real (e.g., log cleanup, backup) and manage it in Git with a proper branch workflow.*

## Phase 2: Containers (Weeks 5–7)
- Docker: images, containers, Dockerfile best practices, multi-stage builds
- docker-compose for multi-container local setups
- Image registries (Docker Hub / cloud registry)

*Milestone: containerize a small app (even a simple web app) with a clean Dockerfile and compose setup.*

## Phase 3: CI/CD (Weeks 8–10)
- Pick GitHub Actions (easiest entry point if you're already using GitHub)
- Build a pipeline: lint → test → build image → push to registry → deploy
- Secrets management in pipelines

*Milestone: fully automated pipeline that deploys your containerized app on every push to main.*

## Phase 4: Cloud Provider (Weeks 11–15)
Pick AWS (most jobs) or GCP (often considered more dev-friendly)
- Compute (EC2/Cloud Run), storage (S3), networking (VPC), IAM
- Get hands-on: deploy your containerized app to the cloud manually first, understand every piece

*Milestone: get a real cloud-hosted deployment of your app, understand your bill and your IAM setup.*

## Phase 5: Infrastructure as Code (Weeks 16–18)
- Terraform: providers, state, plan/apply, modules
- Rebuild the infrastructure from Phase 4 — but in Terraform this time

*Milestone: tear down your manual cloud setup and recreate it entirely from Terraform code.*

## Phase 6: Kubernetes (Weeks 19–24)
This is the deepest, slowest phase — budget more time
- Core objects: pods, deployments, services, ingress
- ConfigMaps, Secrets, namespaces
- Local practice: minikube or kind
- Helm basics for packaging

*Milestone: deploy your app to a local Kubernetes cluster with proper config/secrets separation, then to a managed cluster (EKS/GKE) if budget allows.*

## Phase 7: Monitoring & Observability (Weeks 25–27)
- Prometheus + Grafana for metrics/dashboards
- Basic logging pipeline (Loki or ELK)
- Set up alerts on your running app

*Milestone: dashboard showing real metrics from your deployed app, with an alert that actually fires.*

## Phase 8: Security & polish (Weeks 28–30)
- Secrets management (Vault or cloud-native)
- Basic vulnerability scanning in CI (Trivy, Snyk)
- IAM least-privilege review of everything you built

---

**Total: ~7 months** part-time to genuinely competent. Full-time immersion could compress this to 3-4 months.

**Key principle**: build one project and keep evolving it through every phase rather than doing isolated tutorials. By the end you'll have a single app that went from "runs on my laptop" to "containerized, CI/CD'd, cloud-deployed via Terraform, running in Kubernetes, monitored" — that's a portfolio piece and real understanding at once.

## Linux basics: filesystem, permissions, processes, package managers, systemd. I'm using macOS

Good starting point. Since you're on macOS, first thing: **macOS is Unix-like but not Linux** — similar concepts, different tools underneath. You'll want an actual Linux environment to practice in. Quick options:

- **Docker Desktop** (you'll need this later anyway): `docker run -it ubuntu bash` gives you a disposable Linux shell instantly
- **Multipass** or **UTM** for a real Linux VM
- A cheap cloud VM (AWS free tier, DigitalOcean droplet) — good since production DevOps work is usually remote servers anyway

I'd suggest Docker for now since it's zero setup and you'll install it in Phase 2 regardless.

---

## 1. Filesystem

Linux has a single root tree starting at `/` — no C:\ drives. Key directories:

| Path | What's there |
|---|---|
| `/bin`, `/usr/bin` | executable programs |
| `/etc` | system config files |
| `/home` | user home directories |
| `/var` | logs, variable data (`/var/log` especially) |
| `/tmp` | temp files, cleared on reboot |
| `/opt` | optional/third-party software |
| `/proc` | virtual filesystem exposing running processes/kernel info |

**Commands to get fluent with:**
```bash
ls -la          # list files, including hidden, long format
cd, pwd
cp, mv, rm -rf
find / -name "*.log"     # find files by name
grep -r "error" /var/log # search inside files
cat, less, tail -f       # view files (tail -f for live log watching)
```

macOS note: you already know `ls`/`cd`/`grep` — that part transfers directly since macOS ships BSD versions of these tools. Small flag differences exist (e.g., BSD `sed` vs GNU `sed`) but nothing major at this stage.

## 2. Permissions

This trips people up initially but it's simple once it clicks.

```
-rwxr-xr-x  1 user group  file.sh
```
Three permission groups: **owner / group / others**, each with **read (4) / write (2) / execute (1)**.

```bash
chmod 755 file.sh     # owner: rwx, group: r-x, others: r-x
chmod +x script.sh    # just add execute permission
chown user:group file # change ownership
```

Get comfortable reading `755`, `644`, `600` at a glance — these show up constantly in scripts, Dockerfiles, and SSH key setups (`chmod 600` for private keys is one you'll do a lot).

## 3. Processes

```bash
ps aux              # snapshot of all running processes
top / htop           # live process viewer (htop is nicer, install separately)
kill <pid>           # terminate a process
kill -9 <pid>        # force kill
jobs, fg, bg, &       # foreground/background job control
```

Understand: every process has a PID, a parent process (PPID), and runs as some user. Signals (`SIGTERM` vs `SIGKILL`) matter — `SIGTERM` asks nicely, `SIGKILL` doesn't.

## 4. Package Managers

Different distros, different tools — but same concept (install/update/remove software from repos):

```bash
# Debian/Ubuntu (most common for DevOps work)
apt update && apt install nginx

# RHEL/CentOS/Fedora
yum install nginx
dnf install nginx
```

Ubuntu is the most common target for DevOps tooling, so lean into `apt`.

## 5. systemd

This is how modern Linux manages services (things that should run continuously — web servers, databases, your own apps).

```bash
systemctl start nginx
systemctl stop nginx
systemctl enable nginx     # start automatically on boot
systemctl status nginx     # is it running? recent logs?
journalctl -u nginx -f     # live logs for that service
```

Service configs live in `/etc/systemd/system/*.service` — you'll eventually write your own unit file to run something as a managed service.

---

**Practice exercise to tie it together:**
1. `docker run -it ubuntu bash`
2. `apt update && apt install -y nginx systemd`
3. Look at nginx's default files in `/etc/nginx` and `/var/www`
4. Change permissions on a file, break it, fix it
5. Start nginx, check `ps aux` to see the process, check `systemctl status`
