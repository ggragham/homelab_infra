Base role
=========

Apply firewall rules. Install OpenVPN. Config sftp.

Role Variables
--------------

```yml
# SSH
SSH_PORT: 22  # Set ssh port for firewall
SERVER_SUBNET: 192.168.1.0/24

# OpenVPN
OPENVPN_CONFIG_PATH: ./assets/client.ovpn
VPN_SUBNET: 10.8.0.0/24

# SFTP
SHARE_DISK_GROUP: sharedisk  # Group name for sftp access to ext drive
SHARE_DISK_USER: jdshare  # User name for sftp access to an ext drive
SHARE_PUBLIC_USER: shareuser  # User name for sftp access to public dir on ext drive
DISK_LABEL: disk  # Exd drive label
```

Example Playbook
----------------

```yml
  - hosts: servers
    roles:
       - role: base
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
