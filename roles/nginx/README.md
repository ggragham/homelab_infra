Nginx role
=========

Install and config webserver.

Requirements
------------

- Docker is installed or a Docker Ansible role is applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)). This is required if you choose to use the Dockerized installation of Nginx.

Role Variables
--------------

```yml
NGINX_DOCKERIZED: false  # Nginx dockerized install toogle.
NGINX_VERSION_DOCKER: latest  # Nginx version in Docker (rootless).
NGINX_DOCKER_NETWORK_NAME: '{{ DOCKER_NETWORK_NAME }}'  # Name of the Docker network.

NGINX_DOMAIN_NAME: '{{ DOMAIN_NAME }}'  # Nginx server domain.

SSL_CERT_NAME: cert.crt  # SSL certificate filename placed in the assets/ directory.
SSL_KEY_NAME: cert.key  # SSL Key filename placed in the assets/ directory.
SSL_DH_NAME: dhparam.pem  # DH key filename placed in the assets/ directory.

SSL_CERT_PATH: ./assets/{{ SSL_CERT_NAME }}  # SSL Cert path.
SSL_KEY_PATH: ./assets/{{ SSL_KEY_NAME }}  # SSL Key path.
SSL_DH_PATH: ./assets/{{ SSL_DH_NAME }}  # DH key path.
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
