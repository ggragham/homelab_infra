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
PIHOLE_DOCKER_VERSION: latest  # Pi-hole Docker image version.
PIHOLE_DOCKER_WEBSERVER_PORT: false  # Web server port exposure (false to disable or specify a port number).
PIHOLE_USE_NGINX: false  # Toggle to use Nginx as a reverse proxy for Pi-hole.

PIHOLE_DOMAIN: dns.{{ DOMAIN_NAME }}  # Domain name for the Pi-hole service.
PIHOLE_ADMIN_PASSWORD: foobar123  # Password used to login in Pi-hole WebUI.
PIHOLE_QUERY_LOGGING: 'true'  # Toggle query logging.
PIHOLE_CACHE_SIZE: 10000  # DNS cache size.
PIHOLE_WEBUI_BOXED_LAYOUT: 'true'  # Web interface layout.
PIHOLE_WEBUI_THEME: default-dark  # Web interface theme.
PIHOLE_DNS_RECORDS:  # List of DNS records to be created in Pi-hole.
  - '{{ ansible_host }} {{ DOMAIN_NAME }}'
  - '{{ ansible_host }} {{ PIHOLE_DOMAIN }}'
  - 10.8.0.2 example.com
  - 10.8.0.3 link1.example.com
  - 10.8.0.4 link2.example.com

CLOUDFLARED_DOCKER_IMAGE_VERSION: latest  # Cloudflared Docker image version.
CLOUDFLARED_TUNNEL_DNS_UPSTREAM: https://1.1.1.1/dns-query,https://1.0.0.1/dns-query  # Upstream DoH servers for Cloudflared tunnel.
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
