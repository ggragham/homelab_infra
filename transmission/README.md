Deploy transmission role
=========

Deploy transmission.

Role Variables
--------------

```yml
# SFTP
SHARE_DISK_GROUP: sharedisk  # Group name for sftp access to ext drive
DISK_LABEL: disk  # Exd drive label

# Transmission
TRANSMISSION_SYSTEM_GROUP: debian-transmission  # System group to set directory permissions
TRANSMISSION_PORT: 9091  # Transmission port
TRANSMISSION_USER: transmission  # Username used to login
TRANSMISSION_PASSWORD: 1234  # Password used to login

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
