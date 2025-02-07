# Homelab Infra Ansible Playbooks

<p align="center">
  <a href="https://www.ansible.com/"><img src="https://img.shields.io/badge/ansible-%231A1918.svg?style=for-the-badge&logo=ansible" alt="ansible"></a>
  <a href="https://www.debian.org/"><img src="https://img.shields.io/badge/Debian-D70A53?style=for-the-badge&logo=debian&logoColor=white" alt="debian"></a>
  <br>
  <img src="https://img.shields.io/github/last-commit/ggragham/homelab_infra" alt="last commit">
  <img src="https://img.shields.io/github/repo-size/ggragham/homelab_infra" alt="repo size">
  <a href="http://www.wtfpl.net/about/"><img src="https://img.shields.io/badge/License-WTFPL-brightgreen.svg" alt="license"></a>
</p>

Automate the deployment of my personal Homelab services with Ansible Roles and Playbooks.

# Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
- [Usage](#usage)
- [Playbooks](#playbooks)
- [Roles](#roles)
- [Deployment Options](#deployment-options)
- [Tags](#tags)
- [Author](#author)
- [License](#license)
- [To-Do](#to-do)

# Overview
Homelab Infra Ansible Playbooks provides scripts and roles to deploy and manage self-hosted services on Debian Linux. It supports both Dockerized and bare-metal deployments.

# Prerequisites
* Debian Linux server
* Ansible installed on the control node
* SSH access to the server
* Docker and Docker Compose installed on the server (for Dockerized services)

# Usage
1. Copy the inventory file template (`inventory.ini.template`) to `inventory.ini` and adjust it for your server.
2. Use the default variables file (`default.vars.yml`) and default playbook (`default.playbook.yml`) as templates for your configuration. Rename them as needed (e.g. `master_server.vars.yml`/`master_server.playbook.yml` or `dns_server.vars.yml`/`dns_server.playbook.yml`). These files will be excluded from Git (see [`.gitignore`](./.gitignore)).
3. Place your SSL certificate, SSH key, VPN configuration, etc in the `./assets` directory, and reference them in your variables file.
4. Run your chosen playbook using:
```bash
ansible-playbook master_server.playbook.yml
```
You can also use the `--tags=""` and/or `--skip-tags=""` options to include or exclude tasks. For example:
```bash
ansible-playbook master_server.playbook.yml --tags="base,nextcloud" --skip-tags="nginx"
```

# Playbooks
1. [**default.playbook.yml**](./default.playbook.yml) - Example configuration used as a template.
2. [**playbook_update.yml**](./playbook_update.yml) - Playbook for updating all nodes and rebooting if necessary. Originally authored by [Jeff Geerling](https://github.com/geerlingguy/pi-cluster/blob/master/upgrade.yml).

# Roles
1. [**Nextcloud**](./roles/nextcloud/README.md) - Personal cloud storage solution.
2. [**Gitea**](./roles/gitea/README.md) - Lightweight self-hosted Git service.
3. [**Transmission**](./roles/transmission/README.md) - Fast, easy and free BitTorrent client.
4. [**Pi-hole**](./roles/pihole/README.md) - Network-wide ad blocking via your own Linux hardware.
5. [**Borgmatic**](./roles/borg/README.md) - Simple, configuration-driven backup software for servers and workstations.

## Additional Roles
1. [**Base**](./roles/base/README.md) - Base role for configuring the server, including system updates, essential package installations, VPN setup, disk mounting, and SFTP configuration.
2. [**Nginx**](./roles/nginx/README.md) - High-performance HTTP server and reverse proxy.
3. [**Mariadb**](./roles/mariadb/README.md) - Role for MariaDB installation and configuration.
4. [**Docker**](./roles/docker/README.md) - Role for Docker installation and configuration.

# Deployment Options
The deployment method is determined by the Ansible variable `DOCKERIZED`, which you should set in your `vars.yml` file
* **Dockerized**: Set `DOCKERIZED=true` in your `vars.yml` file for containerized services.
* **Bare Metal**: Set `DOCKERIZED=false` in your `vars.yml` file for direct host installation.

## Supported Deployment Methods
1. **Nextcloud:**
* Dockerized
2. **Gitea:**
* Dockerized
* Bare Metal
3. **Transmission:**
* Dockerized
* Bare Metal
4. **Pi-hole:**
* Dockerized
* Bare Metal
5. **Borgmatic:**
* Bare Metal
6. **Nginx**
* Dockerized
* Bare Metal
7. **MariaDB**
* Dockerized[^1]
* Bare Metal

[^1]: When deploying a Dockerized application that requires MariaDB, the MariaDB service is included in the same docker-compose file and deployed together with the application.

# Tags
Tags are used to control which tasks are executed during playbook run. Here is a list of available tags and their descriptions:
* **base** - Tasks for general system configuration and updates.
* **nginx** - Tasks for installing and configuring the Nginx web server.
* **mariadb** - Tasks for setting up the MariaDB database server.
* **docker** - Tasks for Docker installation and service management.
* **nextcloud** - Tasks for deploying the Nextcloud personal cloud storage solution.
* **gitea** - Tasks for setting up the Gitea self-hosted Git service.
* **transmission** - Tasks for installing the Transmission BitTorrent client.
* **pihole** - Tasks for deploying the Pi-hole network-wide ad blocker.
* **borg** - Tasks for setting up the Borgmatic backup software.

# Author
This project was created by [Grell Gragham](https://github.com/ggragham).

# License
This software is published under the DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE license.

# To-Do
- [ ] Implement database backup functionality using Borgmatic.
- [ ] Implement Jellyfin deployment.
- [ ] Move Pi-Hole deployment to a dedicated repository.
