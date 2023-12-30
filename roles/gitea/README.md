Gitea role
=========

Install and config Gitea git server.

Role Variables
--------------

```yml
GITEA_DOMAIN: git.{{ DOMAIN_NAME }}
GITEA_APP_NAME: tea
GITEA_PORT: 3000
GITEA_USER: gitea_user
GITEA_PATH: /opt/gitea
GITEA_DATA_PATH: /mnt/{{ DISK_LABEL }}/gitea
GITEA_CONFIG_PATH: /etc/gitea
GITEA_DB_NAME: giteadb
GITEA_DB_USER: gitea_db_user
GITEA_DB_PASSWORD: gitea_db_password
GITEA_PASSWORD_HASH_ALGO: pbkdf2
GITEA_LFS_JWT_SECRET: N1tudjNy+lnpUb4HjhVDZnrkIw0LBfuwxK4Pr1tJ
GITEA_INTERNAL_TOKEN: cgCZZhsH9Y6pYMt8Gp5KfSNqF1Msydd_Zzpal6SwF4HMSGN86ZT2qHjfsQ7y64cPV1ev7HF/jygkFEVvfiCzrKA
```

Dependencies
------------

```yml
dependencies:
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
