Redmine Role
============

Install and configure Redmine.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)).

Role Variables
--------------

```yml
REDMINE_DOCKER_TAG: latest  # Redmine Docker image tag.
REDMINE_DOCKER_HTTP_PORT: 8080  # Redmine WebUI HTTP port.

REDMINE_TIMEZONE: Etc/UTC  # Redmine timezone.
REDMINE_LANG: en  # Redmine default language.

REDMINE_SECRET_KEY_BASE: change_me_to_long_random_secret  # Redmine secret key base. Change it to a long random value.

REDMINE_DB_HOST: 192.168.88.128  # Redmine database host.
REDMINE_DB_PORT: 3306  # Redmine database port.
REDMINE_DB_USERNAME: redmine  # Redmine database username.
REDMINE_DB_PASSWORD: redmine_password  # Redmine database password.
REDMINE_DB_DATABASE: redmine  # Redmine database name.
REDMINE_DB_ENCODING: utf8mb4  # Redmine database encoding.
```

Dependencies
------------

```yml
dependencies:
  - role: docker
```

Example Playbook
----------------

```yml
  - hosts: redmine-node
    roles:
       - role: redmine
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
