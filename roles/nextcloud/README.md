NextCloud role
=========

Install and config NextCloud.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)).
- A MariaDB instance must be installed, or a MariaDB Ansible role must be applied (see [MariaDB Installation Guide](https://mariadb.com/kb/en/getting-installing-and-upgrading-mariadb/)). If `NEXTCLOUD_DOCKERIZED: true`, MariaDB will be included in the same Docker Compose file as part of the deployment.
- NGINX must be installed, or an NGINX Ansible role must be applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)), if `NEXTCLOUD_USE_NGINX: true`.

Role Variables
--------------

```yml
NEXTCLOUD_DOCKERIZED: true  #  Toggle for Docker setup.
NEXTCLOUD_DOCKER_VERSION: stable  # NextCloud Docker image version.
NEXTCLOUD_DOCKER_NETWORK_NAME: '{{ DOCKER_NETWORK_NAME }}'  # Name of the Docker network.

NEXTCLOUD_USE_NGINX: false  # Toggle to use Nginx as a reverse proxy for NextCloud.
NEXTCLOUD_DOCKER_WEBSERVER_PORT: false  # Nextcloud web server port configuration (set to false to disable, or specify a port number).
NEXTCLOUD_DOMAIN: cloud.{{ DOMAIN_NAME }}  # Domain name for the NextCloud service.
NEXTCLOUD_PORT: 9001  # Nextcloud service port.
NEXTCLOUD_DATA_PATH: '{{ DISK_DATA_PATH }}/nextcloud'  # Nextcloud data path.
NEXTCLOUD_MAX_FILE_SIZE: 4G  # Maximum upload file size.

NEXTCLOUD_DOCKER_MARIADB_VERSION: lts  # MariaDB Docker image version.
NEXTCLOUD_DB_ROOT_PASSWORD: root1234!  # MariaDB root-user password.
NEXTCLOUD_DB_NAME: nextclouddb  # Nextcloud database name.
NEXTCLOUD_DB_USER: nextclouduser  # Nextcloud database user.
NEXTCLOUD_DB_PASSWORD: qwerty1234!  # Nextcloud database password.
```

Dependencies
------------

```yml
dependencies:
  - role: docker
  - role: mariadb
  - role: nginx  # Optional
```

Example Playbook
----------------

```yml
  - hosts: servers
    roles:
       - role: nextcloud
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
