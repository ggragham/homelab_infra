# Homelab Infra Ansible Playbooks

<p>
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
- [Author](#author)
- [License](#license)

# Overview
Homelab Infra Ansible Playbooks provides scripts and roles to deploy and manage self-hosted services. It supports both Dockerized and bare-metal deployments.

# Prerequisites
* Linux server
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

# Playbooks
* [**default.playbook.yml**](./default.playbook.yml) - Example configuration used as a template.
* [**playbook_update.yml**](./playbook_update.yml) - Playbook for updating all nodes and rebooting if necessary. Originally authored by [Jeff Geerling](https://github.com/geerlingguy/pi-cluster/blob/master/upgrade.yml).

# Roles
* [**Nginx**](./roles/nginx/README.md) - High-performance HTTP server and reverse proxy.
* [**Nginx Proxy Manager**](./roles/nginx_proxy_manager/README.md) - Reverse proxy management with a user-friendly web interface.
* [**MariaDB**](./roles/mariadb/README.md) - Role for MariaDB installation and configuration.
* **(WIP)** [**Borgmatic**](./roles/borg/README.md) - Simple, configuration-driven backup software for servers and workstations.
* [**Pi-hole**](./roles/pihole/README.md) - Network-wide ad blocking via your own Linux hardware.
* [**Gitea**](./roles/gitea/README.md) - Lightweight self-hosted Git service.
* [**Nextcloud**](./roles/nextcloud/README.md) - Personal cloud storage solution.
* [**Transmission**](./roles/transmission/README.md) - Fast, easy and free BitTorrent client.

> Detailed usage, variables, and examples are documented in each role’s own README.

## External Roles
* [**base**](https://github.com/youruser/base_ansible_role) – external role for initial server setup.
* [**hardening**](https://github.com/youruser/hardening_ansible_role) – external role for applying security hardening.

# Deployment Options
The deployment method for each service is determined by its individual Ansible variable `<SERVICE_NAME>_DOCKERIZED`, which you should set in your `vars.yml` file. For each service, choose:
* **Dockerized**: Set `<SERVICE_NAME>_DOCKERIZED: true` to deploy the service as a containerized application.
* **Bare Metal**: Set `<SERVICE_NAME>_DOCKERIZED: false` to deploy the service directly on the host.

For example:
- To deploy Nextcloud in a containerized manner, set `NEXTCLOUD_DOCKERIZED: true`.
- To deploy Gitea on the host (bare metal), set `GITEA_DOCKERIZED: false`.

## Supported Deployment Methods
* Nginx: Dockerized, Bare Metal
* Nginx Proxy Manager: Dockerized
* MariaDB: Dockerized[^1], Bare Metal
* Borgmatic (WIP): Bare Metal
* Pi-hole: Dockerized, Bare Metal
* Gitea: Dockerized, Bare Metal
* Nextcloud: Dockerized
* Transmission: Dockerized, Bare Metal

[^1]: When deploying a Dockerized application that requires MariaDB, the MariaDB service is included in the same docker-compose file and deployed together with the application.

# Author
This project was created by [Grell Gragham](https://github.com/ggragham).

# License
This software is published under the DO WHAT THE FUCK YOU WANT TO PUBLIC LICENSE license.
