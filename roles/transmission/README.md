Deploy transmission role
=========

Deploy Transmission torrent client.

Requirements
------------

- Docker is installed or a Docker Ansible role is applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)). This is required if you choose to use the Dockerized installation.

Role Variables
--------------

```yml
# SFTP
SHARE_DISK_GROUP: sharedisk  # Group name for sftp access to ext drive
DISK_LABEL: disk  # Exd drive label

# Transmission
TRANSMISSION_DOMAIN: torrent.{{ DOMAIN_NAME }}  # Domain name for the Transmission service
TRANSMISSION_DOCKER_VERSION: latest  # Transmission Docker image version.
TRANSMISSION_PORT: 9091  # Transmission port
TRANSMISSION_PEER_PORT: 51413  # Transmission peer port
TRANSMISSION_USER: transmission  # Username used to login
TRANSMISSION_PASSWORD: qwerty1234!  # Password used to login
TRANSMISSION_DATA_PATH: '{{ DISK_DATA_PATH }}/transmission'  # Transmission data directory path
```

Dependencies
------------

```yml
dependencies:
  - role: docker  # Optional
  - role: nginx
```

Example Playbook
----------------

```yml
  - hosts: servers
    roles:
       - role: transmission
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
