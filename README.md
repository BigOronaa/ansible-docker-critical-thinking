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

