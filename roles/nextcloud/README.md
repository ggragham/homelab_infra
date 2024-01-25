NextCloud role
=========

Install and config NextCloud.

Requirements
------------

- Docker is installed or a Docker Ansible role is applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)).
- MariaDB is installed or an MariaDB Ansible role is applied (see [MariaDB Installation Guide](https://mariadb.com/kb/en/getting-installing-and-upgrading-mariadb/)).
- NGINX is installed or an NGINX Ansible role is applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)).

Role Variables
--------------

```yml
# Other
DOCKERIZED: false  #  Toggle for Docker setup.
DISK_LABEL: disk  # External disk label.

# NextCloud
NEXTCLOUD_DATA_PATH: '{{ DISK_DATA_PATH }}/nextcloud'  # Nextcloud data path.
NEXTCLOUD_DOMAIN: cloud.{{ DOMAIN_NAME }}  # Nextcloud domain name.
NEXTCLOUD_DOCKER_VERSION: stable  # NextCloud Docker image version.
NEXTCLOUD_PORT: 9001  # Nextcloud service port.
NEXTCLOUD_MAX_FILE_SIZE: 4G  # Maximum upload file size.
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
  - role: nginx
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
