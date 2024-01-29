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
Homelab Infra Ansible Playbooks is a set of scripts and roles designed for deploying and managing self-hosted services within a homelab environment, primarily on Debian Linux. The playbooks automate the deployment of various services, with some services offering both containerized (Docker) and bare metal installation options. For Dockerized services, Docker Compose is used for deployment.

# Prerequisites
* Debian Linux server
* Ansible installed on the control node
* SSH access to the server
* Docker and Docker Compose installed on the server (for Dockerized services)

# Usage
0. If you are setting up a new server, you can use the initial configuration playbook and role provided in the `_init/` directory.
1. Make a copy of the inventory file template (`inventory.ini.template`) and rename it to `inventory.ini`. Configure it according to your server setup.
2. Make a copy of the vars file template (e.g., `./vars/vars.yml.template`) and rename it to `vars.yml`. Then, open the file and set the variables according to your server and service setup.
3. Place your SSL certificate, SSH key, and VPN configuration file in the `./assets` directory. Don't forget to specify the names of these files in the `vars.yml` file.
4. Use the `ansible-playbook` command to run the desired playbook. For example:
```bash
ansible-playbook playbook.yml
```
You can also use the `--tags=""` and/or `--skip-tags=""` options to include or exclude tasks. For example:
```bash
ansible-playbook playbook.yml --tags="base,nextcloud" --skip-tags="firewall"
```
Refer to the [Playbooks](#playbooks) section for a list of available playbooks and their descriptions. For information about tags, see the [Tags](#tags) section.

# Playbooks
1. [**playbook.yml**](./playbook.yml) - Main playbook for deploying the master server with various services like Nextcloud, Gitea, etc.
2. [**playbook_dns.yml**](./playbook_dns.yml) - Playbook for deploying a DNS server with Pi-hole.
3. [**playbook_backup.yml**](./playbook_backup.yml) - Playbook for deploying a backup server with Borgmatic.
4. [**playbook_update.yml**](./playbook_update.yml) - Playbook for updating all nodes and rebooting if necessary. Originally authored by [Jeff Geerling](https://github.com/geerlingguy/pi-cluster/blob/master/upgrade.yml).

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
* **prepare** - Tasks for initial server setup, including SSH configuration.
* **firewall** - Tasks for setting up server firewall rules and policies.
* **openvpn** - Tasks for installing and configuring OpenVPN.
* **disk** - Tasks for mounting disk drives and setting up file systems.
* **sftp** - Tasks for setting up secure file transfer via SFTP.
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
