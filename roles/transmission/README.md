Deploy transmission role
=========

Deploy Transmission torrent client.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)), if `TRANSMISSION_DOCKERIZED: true`.
- NGINX must be installed, or an NGINX Ansible role must be applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)), if `TRANSMISSION_USE_NGINX: true`.

Role Variables
--------------

```yml
TRANSMISSION_DOCKERIZED: true  # Transmission dockerized install toogle.
TRANSMISSION_DOCKER_VERSION: latest  # Transmission Docker image version.
TRANSMISSION_DOCKER_NETWORK_NAME: '{{ DOCKER_NETWORK_NAME }}'  # Name of the Docker network.
TRANSMISSION_DOCKER_WEBSERVER_PORT: false  # Transmission web server port configuration (set to false to disable, or specify a port number).

TRANSMISSION_USE_NGINX: false  # Toggle to use Transmission as a reverse proxy for Gitea.
TRANSMISSION_DATA_PATH: '{{ DISK_DATA_PATH }}/transmission'  # Transmission data directory path.

TRANSMISSION_DOMAIN: torrent.{{ DOMAIN_NAME }}  # Domain name for the Transmission service.
TRANSMISSION_PORT: 9091  # Transmission port.
TRANSMISSION_PEER_PORT: 51413  # Transmission peer port.

TRANSMISSION_USER: transmission  # Username used to login.
TRANSMISSION_PASSWORD: qwerty1234!  # Password used to login.
```

Dependencies
------------

```yml
dependencies:
  - role: docker  # Optional
  - role: nginx  # Optional
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
