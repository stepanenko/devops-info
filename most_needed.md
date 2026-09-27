## The 20% of DevOps that is used 80% of the time

As a beginner, you don’t need to learn everything. Focus on the small set of skills that appear in almost every real DevOps job, project, and daily workflow. Master these and you will already be useful.

Here is the practical 20%:

### 1. Git (Version Control)

Almost every change starts with Git. You will use it every single day.

- Basic commands: `clone`, `add`, `commit`, `push`, `pull`, `branch`, `merge`, `rebase`
- Pull requests / merge requests
- Simple branching strategy (main + feature branches)

### 2. Linux Command Line + Basic Scripting

Servers, containers, and cloud instances almost always run Linux. You will live in the terminal.

- Navigating files (`cd`, `ls`, `pwd`, `mkdir`, `rm`)
- Viewing and editing files (`cat`, `less`, `nano` or `vim`)
- Permissions, processes, and basic networking (`ps`, `top`, `curl`, `ssh`)
- Simple Bash scripts

### 3. Docker (Containers)

Almost every modern application runs in containers. You will build, run, and debug containers daily.

- What a container is and why it is useful
- `Dockerfile` basics
- Commands: `build`, `run`, `ps`, `logs`, `exec`
- Docker Compose for running multiple services locally

### 4. CI/CD Pipelines

This is the heart of modern DevOps. Code is automatically built, tested, and deployed.

- What Continuous Integration and Continuous Delivery mean
- How a basic pipeline works (build → test → deploy)
- One tool deeply: **GitHub Actions** or **GitLab CI** (they are the most common for beginners)
- How to read and write a simple pipeline file (YAML)

### 5. Cloud Fundamentals (AWS, Azure, or GCP — pick one)

Most companies run on the cloud. You need to understand the main building blocks.

- Compute (virtual machines / instances)
- Storage
- Networking (VPC, subnets, security groups)
- Identity and access (IAM)

### 6. Infrastructure as Code (IaC) – Terraform basics

Modern teams no longer click around in cloud consoles. They describe infrastructure in code.

- What Infrastructure as Code means
- Basic Terraform: providers, resources, variables, state
- How to create simple resources (a server, a network, a storage bucket)

### 7. Monitoring & Logging (Observability basics)

You cannot improve or fix what you cannot see. Every production system needs monitoring.

- The difference between metrics, logs, and traces
- Basic concepts: alerts, dashboards, uptime
- One popular stack at a high level (e.g. Prometheus + Grafana, or cloud monitoring tools)

---

### Recommended Learning Order (most important first)

1. Git  
2. Linux basics  
3. Docker  
4. CI/CD (GitHub Actions)  
5. Cloud fundamentals  
6. Terraform  
7. Monitoring basics  

---

**Key mindset**  
These seven areas cover the vast majority of daily DevOps work. Once you are comfortable with them, the remaining 80% of tools and advanced topics become much easier to learn when you need them.
