Nginx role
=========

Install and config webserver.

Role Variables
--------------

```yml
# SSH
SSH_PORT: 22  # Set ssh port for firewall
SERVER_SUBNET: 192.168.1.0/24

# NGINX
SSL_CERT_NAME: cert.crt # SSL Cert name
SSL_KEY_NAME: cert.key # SSL Key name
DH_NAME: dhparam.pem # DH group name

SSL_CERT_PATH: ./assets/{{ SSL_CERT_NAME }} # SSL Cert path
SSL_KEY_PATH: ./assets/{{ SSL_KEY_NAME }} # SSL Key path
DH_PATH: ./assets/{{ DH_NAME }} # DH group path
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
