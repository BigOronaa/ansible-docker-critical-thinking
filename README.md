# Critical Thinking: Configuring Docker Containers with Ansible

This project automates the installation of Docker and the deployment of
containerized services (Nginx, MySQL, Redis) across different environments
using Ansible and GitHub Actions.

Environments:
- Development
- Staging
- Production


## Architecture
- AWS EC2 (Ubuntu)
- Ansible (control node via WSL)
- Docker Engine
- Containers:
  - Nginx (web)
  - MySQL (database)
  - Redis (cache)

## Project Structure
- inventories/
- group_vars/
- roles/
  - docker
  - webserver
  - database
  - cache
- playbooks/site.yml

## Steps I Took
1. I created an EC2 instance and configured SSH access.
2. I set up Ansible inventory and configuration.
3. I created a Docker role to install and configure Docker.
4. I created a Webserver role to deploy Nginx.
5. I created a Database role to deploy MySQL with environment variables.
6. I created a Cache role to deploy Redis.
7. I verified idempotency by re-running the playbook.
8. I validated running containers on the EC2 host.

## Tools and Technologies
- Ansible (ansible-core)
- Docker
- GitHub Actions (CI/CD)
- AWS EC2 (Linux/Ubuntu)
- community.docker Ansible collection

## Repository Structure
```
ansible-docker-critical-thinking/
├── inventories/
│   ├── dev.ini
│   ├── staging.ini
│   └── production.ini
├── group_vars/
│   ├── dev.yml
│   ├── staging.yml
│   └── prod.yml
├── roles/
│   ├── docker/
│   ├── webserver/
│   ├── database/
│   └── cache/
├── playbooks/
│   ├── site.yml
│   └── monitor.yml
├── .github/workflows/
│   └── deploy.yml
└── README.md
```

## Setting Up Docker with Ansible
- Docker is installed using an Ansible role.
- Required system packages are installed.
- Docker repository and GPG keys are added.
- Docker service is enabled and started.
- The `ubuntu` user is added to the Docker group.

---

## Container Deployment
Each service is deployed using a dedicated Ansible role:
- **Webserver Role**: Deploys Nginx container and exposes HTTP ports.
- **Database Role**: Deploys MySQL container with environment variables for credentials.
- **Cache Role**: Deploys Redis container.

Ansible modules such as `docker_image` and `docker_container` are used for automation.

---

## Environment-Specific Configuration
Environment-specific values (ports, credentials, container names) are defined using:
- `inventories/*.ini`
- `group_vars/*.yml`

This ensures each environment (dev, staging, production) can have unique configurations while using the same playbooks.

---

## Automated Deployment with GitHub Actions
- CI/CD pipeline runs on pushes to `dev`, `staging`, and `master` branches.
- SSH authentication is handled using GitHub Secrets.
- Ansible playbooks are executed automatically based on the branch pushed.
- Host key checking is disabled to prevent SSH interruptions in CI.

---

## Monitoring and Logging
- An Ansible monitoring playbook checks container availability.
- Docker logs are collected using Ansible commands.
- The playbook fails if expected containers are not running.

---

## Troubleshooting Guide
Common issues and resolutions:
- **SSH timeout**: Ensure EC2 security group allows port 22 from GitHub runners.
- **Container not found**: Verify container names match those defined in roles.
- **Workflow failures**: Check inventory files and SSH key configuration.
- **IP changes**: Update inventory files when EC2 public IPs change.

---

## How to Trigger Deployment
1. Push code to the appropriate branch:
   - `dev` → Development environment
   - `staging` → Staging environment
   - `master` → Production environment
2. GitHub Actions automatically runs the Ansible deployment workflow.

---