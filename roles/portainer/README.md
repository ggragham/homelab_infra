Portainer Role
==============

Install and configure Portainer.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)).

Role Variables
--------------

```yml
PORTAINER_DOCKER_VERSION: sts  # Portainer Docker image version.
PORTAINER_DOCKER_HTTP_PORT: 9443  # Portainer WebUI HTTP port.
PORTAINER_DOCKER_EDGE_AGENTS_PORT: 8000  # Portainer edge agents port for remote management (set to false to disable, or specify a port number).
PORTAINER_DOCKER_USE_NGINX: false  # Toggle to use Nginx as a reverse proxy for Portainer.

PORTAINER_DOMAIN: portainer.{{ DOMAIN_NAME }}  # Domain name for the Portainer service.
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
  - hosts: portainer-node
    roles:
       - role: portainer
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
