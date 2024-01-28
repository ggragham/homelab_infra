Gitea role
=========

Install and config Gitea git server.

Requirements
------------

- Docker is installed or a Docker Ansible role is applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)). This is required if you choose to use the Dockerized installation.
- MariaDB is installed or an MariaDB Ansible role is applied (see [MariaDB Installation Guide](https://mariadb.com/kb/en/getting-installing-and-upgrading-mariadb/)).
- NGINX is installed or an NGINX Ansible role is applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)).

Role Variables
--------------

```yml
# Other
DOCKERIZED: false  #  Toggle for Docker setup.
DISK_LABEL: disk  # External disk label

# Gitea
GITEA_CHECK_UPDATES: false  # Controls Gitea's update checks.
GITEA_DOMAIN: git.{{ DOMAIN_NAME }}  # Gitea's domain name.
GITEA_APP_NAME: tea  # Name of Gitea application.
GITEA_PORT: 3000  # Gitea's running port.
GITEA_USER: gitea_user  # Gitea system username.
GITEA_ID: 1030  # Gitea system UID/GID.
GITEA_DB_NAME: giteadb  # Gitea's database name.
GITEA_DB_USER: gitea_db_user  # Gitea's database username.
GITEA_DB_PASSWORD: gitea_db_password  # Gitea's database password.
GITEA_PASSWORD_HASH_ALGO: pbkdf2  # Gitea's password hashing algorithm.
GITEA_LFS_JWT_SECRET: N1tudjNy+lnpUb4HjhVDZnrkIw0LBfuwxK4Pr1tJ  # Secret key for Gitea's Large File Storage JWT authentication.
GITEA_INTERNAL_TOKEN: cgCZZhsH9Y6pYMt8Gp5KfSNqF1Msydd_Zzpal6SwF4HMSGN86ZT2qHjfsQ7y64cPV1ev7HF/jygkFEVvfiCzrKA  # Gitea's internal token.
GITEA_JWT_SECRET: QTi5BTxUyLEjc36PNSsk7QfFGYi3qmkExPu4kHlVv20d3+0Cl7D5r7KwqpA=  # Secret key for Gitea's JWT authentication.

GITEA_ADMIN_USER: gitea_admin  # Username for the Gitea administrator account.
GITEA_ADMIN_EMAIL: gitea_admin@{{ DOMAIN_NAME }}  # Email address for the Gitea administrator account.
GITEA_ADMIN_PASSWORD: qwerty1234!  # Password for the Gitea administrator account.

ACT_VERSION: latest  # act_runner version.
ACT_REREGISTER_RUNNER: false  # Re-register runner.
```

Dependencies
------------

```yml
dependencies:
  - role: docker  # Optional
  - role: mariadb
  - role: nginx
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
