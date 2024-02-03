Pi-hole role
=========

Install and config Pi-hole DNS server.

Requirements
------------
- Docker is installed or a Docker Ansible role is applied (see [Docker Installation Guide](https://docs.docker.com/engine/install/)). This is required if you choose to use the Dockerized installation.
- NGINX is installed or an NGINX Ansible role is applied (see [NGINX Installation Guide](https://nginx.org/en/docs/install.html)).

Role Variables
--------------

```yml
PIHOLE_DOMAIN: dns.{{ DOMAIN_NAME }}  # Domain name for the Pi-hole service.
PIHOLE_DOCKER_VERSION: latest  # Pi-hole Docker image version.
PIHOLE_ADMIN_PASSWORD: qwerty1234!  # Password used to login in Pi-hole WebUI.

PIHOLE_INTERFACE: eth0  # Network interface for Pi-hole.
PIHOLE_DNS_1: 1.1.1.1  # Primary DNS server.
PIHOLE_DNS_2: 1.0.0.1  # Secondary DNS server.
PIHOLE_DNS_3: 9.9.9.9  # Tertiary DNS server.
PIHOLE_DNS_4: 149.112.112.112  # Quaternary DNS server.
PIHOLE_QUERY_LOGGING: 'true'  # Toggle query logging.
PIHOLE_INSTALL_WEB_INTERFACE: 'true'  # Toggle web interface installation.
PIHOLE_CACHE_SIZE: 10000  # DNS cache size.
PIHOLE_WEBUI_BOXED_LAYOUT: boxed  # Web interface layout.
PIHOLE_WEBTHEME: default-dark  # Web interface theme.
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
       - role: pihole
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
