Pi-hole role
=========

Install and config Pi-hole DNS server.

Requirements
------------

- Docker must be installed, or a Docker Ansible role must be applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)), if `PIHOLE_DOCKERIZED: true`.
- NGINX must be installed, or an NGINX Ansible role must be applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)), if `PIHOLE_USE_NGINX: true`.

Role Variables
--------------

```yml
PIHOLE_DOCKERIZED: true  # Pihole dockerized install toogle.
PIHOLE_DOCKER_NETWORK_NAME: '{{ DOCKER_NETWORK_NAME }}'  # Name of the Docker network.
PIHOLE_DOCKER_WEBSERVER_PORT: false  # Web server port exposure (false to disable or specify a port number).
PIHOLE_USE_NGINX: false  # Toggle to use Nginx as a reverse proxy for Pi-hole.
PIHOLE_DOMAIN_NAME: '{{ DOMAIN_NAME }}'
PIHOLE_DOMAIN: dns.{{ PIHOLE_DOMAIN_NAME }}  # Domain name for the Pi-hole service.
PIHOLE_DOCKER_VERSION: latest  # Pi-hole Docker image version.
PIHOLE_ADMIN_PASSWORD: qwerty1234!  # Password used to login in Pi-hole WebUI.

PIHOLE_DNS_1: 1.1.1.1  # Primary DNS server.
PIHOLE_DNS_2: 1.0.0.1  # Secondary DNS server.
PIHOLE_DNS_3: 9.9.9.9  # Tertiary DNS server.
PIHOLE_DNS_4: 149.112.112.112  # Quaternary DNS server.
PIHOLE_QUERY_LOGGING: 'true'  # Toggle query logging.
PIHOLE_CACHE_SIZE: 10000  # DNS cache size.
PIHOLE_WEBUI_BOXED_LAYOUT: boxed  # Web interface layout.
PIHOLE_WEBTHEME: default-dark  # Web interface theme.

PIHOLE_DNS_RECORDS:  # List of DNS records to be created in Pi-hole.
  - '{{ ansible_host }} {{ PIHOLE_DOMAIN_NAME }}'
  - '{{ ansible_host }} {{ PIHOLE_DOMAIN }}'

## Only for baremetal installation. 
PIHOLE_INTERFACE: '{{ NETWORK_INTERFACE }}'  # Network interface for Pi-hole.
PIHOLE_INSTALL_WEB_INTERFACE: 'true'  # Toggle web interface installation.
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
       - role: pihole
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
