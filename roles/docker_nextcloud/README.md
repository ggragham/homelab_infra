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
NEXTCLOUD_DOMAIN: cloud.{{ DOMAIN_NAME }}
NEXTCLOUD_DOCKER_VERSION: 28-fpm-alpine
NEXTCLOUD_PORT: 9001
NEXTCLOUD_PATH: /var/www/html/nextcloud
NEXTCLOUD_MAX_FILE_SIZE: 4G
NEXTCLOUD_DB_NAME: nextclouddb
NEXTCLOUD_DB_USER: nextclouduser
NEXTCLOUD_DB_PASSWORD: qwerty1234!
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
