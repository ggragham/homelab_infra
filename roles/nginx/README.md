Nginx role
=========

Install and config webserver.

Requirements
------------

- Docker is installed or a Docker Ansible role is applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)). This is required if you choose to use the Dockerized installation of Nginx.

Role Variables
--------------

```yml
---
# Other
DOCKERIZED: false  #  Toggle for Docker setup

# NGINX
DOMAIN_NAME: example.com  # Nginx server domain

SSL_CERT_NAME: cert.crt  # SSL Cert name
SSL_KEY_NAME: cert.key  # SSL Key name
DH_NAME: dhparam.pem  # DH group name

SSL_CERT_PATH: ./assets/{{ SSL_CERT_NAME }}  # SSL Cert path
SSL_KEY_PATH: ./assets/{{ SSL_KEY_NAME }}  # SSL Key path
DH_PATH: ./assets/{{ DH_NAME }}  # DH group path

NGINX_DOCKER_PATH: /opt/nginx_docker # Dockerized Nginx Path
NGINX_VERSION_DOCKER: latest # Nginx version in Docker
```

Dependencies
------------

```yml
dependencies:
  - role: docker  # Optional
```


Example Playbook
----------------

```yml
  - hosts: servers
    roles:
       - role: nginx
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
