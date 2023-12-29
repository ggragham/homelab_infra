Deploy transmission role
=========

Deploy Transmission torrent client.

Role Variables
--------------

```yml
TRANSMISSION_DOMAIN: torrent.{{ DOMAIN_NAME }}  # Domain name for the Transmission service
TRANSMISSION_SYSTEM_GROUP: debian-transmission  # System group to set directory permissions
TRANSMISSION_PORT: 9091  # Transmission port
TRANSMISSION_USER: transmission  # Username used to login
TRANSMISSION_PASSWORD: 1234  # Password used to login
```

Dependencies
------------

```yml
dependencies:
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
