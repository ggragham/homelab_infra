Gitea role
=========

Install and config Gitea git server.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)), if `GITEA_DOCKERIZED: true`.
- A MariaDB instance must be installed, or a MariaDB Ansible role must be applied (see [MariaDB Installation Guide](https://mariadb.com/kb/en/getting-installing-and-upgrading-mariadb/)). If `GITEA_DOCKERIZED: true`, MariaDB will be included in the same Docker Compose file as part of the deployment.
- NGINX must be installed, or an NGINX Ansible role must be applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)), if `GITEA_USE_NGINX: true`.

Role Variables
--------------

```yml
GITEA_DEPLOY: "{{ inventory_hostname == 'gitea_host' }}"  # Service variable. For separate installation Gitea and ActRunner by host.
GITEA_IP: 192.168.1.30

GITEA_DOCKERIZED: true  # Gitea dockerized install toogle.
GITEA_DOCKER_VERSION: latest  # Gitea Docker image version (rootless).
GITEA_DOCKER_NETWORK_NAME: '{{ DOCKER_NETWORK_NAME }}'  # Name of the Docker network.

GITEA_USE_NGINX: false  # Toggle to use Nginx as a reverse proxy for Gitea.
GITEA_APP_NAME: tea  # Name of Gitea application.
GITEA_ADMIN_USER: gitea_admin  # Username for the Gitea administrator account.
GITEA_ADMIN_EMAIL: gitea_admin@{{ DOMAIN_NAME }}  # Email address for the Gitea administrator account.
GITEA_ADMIN_PASSWORD: qwerty1234!  # Password for the Gitea administrator account.
GITEA_LFS_JWT_SECRET: example_of_lfs_jwt_secret  # Secret key for Gitea's Large File Storage JWT authentication.
GITEA_INTERNAL_TOKEN: example_of_internal_token  # Gitea's internal token.
GITEA_JWT_SECRET: example_of_jwt_key  # Secret key for Gitea's JWT authentication.

GITEA_DOMAIN: git.{{ DOMAIN_NAME }}  # Gitea's domain name.
GITEA_PORT: 3000  # Gitea's running port.
GITEA_DATA_PATH: '{{ DISK_DATA_PATH }}/gitea'  # Gitea's data storage path.
GITEA_CHECK_UPDATES: false  # Controls Gitea's update checks.
GITEA_PASSWORD_HASH_ALGO: pbkdf2  # Gitea's password hashing algorithm.

GITEA_DOCKER_MARIADB_VERSION: lts  # MariaDB Docker image version.

GITEA_DB_DEPLOY: false  # Toggle to include database service in Docker Compose.
GITEA_DB_HOST: '{{ GITEA_DOCKER_DB_SERVICE_NAME }}'  # Database host for Gitea.
GITEA_DB_PORT: 3306  # Port for the Gitea database server.
GITEA_DB_ROOT_PASSWORD: root1234!  # MariaDB root-user password.
GITEA_DB_NAME: giteadb  # Gitea's database name.
GITEA_DB_USER: gitea_db_user  # Gitea's database username.
GITEA_DB_PASSWORD: gitea_db_password  # Gitea's database password.

ACTRUNNER_DEPLOY: "{{ inventory_hostname == 'actrunner_host' }}"  # Service variable. For separate installation Gitea and ActRunner.

ACT_VERSION: latest  # act_runner version.
ACT_REREGISTER_RUNNER: false  # Re-register runner.
```

Dependencies
------------

```yml
dependencies:
  - role: docker  # Optional
  - role: mariadb
  - role: nginx  # Optional
```

Example Playbook
----------------

```yml
  - hosts: servers
    roles:
       - role: gitea
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
