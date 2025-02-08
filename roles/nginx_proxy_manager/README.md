Nginx Proxy Manager Role
=========

Install and config Nginx Proxy Manager.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)).

Role Variables
--------------

```yml
NPM_DOCKERIZED: true  # Nginx Proxy Manager dockerized install toogle.
NPM_DOCKER_VERSION: latest  # Nginx Proxy Manager Docker image version.
NPM_DOCKER_NETWORK_NAME: '{{ DOCKER_NETWORK_NAME }}'  # Name of the Docker network.
NPM_DOMAIN: proxy.{{ PIHOLE_DOMAIN_NAME }}  # Domain name for the Nginx Proxy Manager service.
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
  - hosts: servers
    roles:
       - role: npm
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
