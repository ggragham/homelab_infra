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
OPENVPN_ENABLED: false
OPENVPN_CONFIG_PATH: '{{ ASSETS_PATH }}/client.ovpn'
OPENVPN_PORT: 1194
VPN_SUBNET: 10.8.0.0/24

# External Disk
EXT_DISK_ENABLED: true  # Enables or disables external disk mounting
DISK_LABEL: disk  # External disk label
DISK_ENCRYPTED: false  # Disk encryption status
DISK_KEYFILE: keyfile.pem  # Encryption key file name
DISK_KEYFILE_PATH: '{{ ASSETS_PATH }}/{{ DISK_KEYFILE }}'  # Path to encryption key file
DISK_FSTYPE: btrfs  # Disk filesystem type

DISK_SUBVOLS:  # List of BTRFS subvolumes
  - name: storage
    subvol: '@storage'  # Subvolume name in filesystem
    path: /mnt/{{ DISK_LABEL }}/storage  # Subvolume mount point
    compression: zstd:1  # Subvolume compression

# SFTP
SHARING_ENABLED: false  # Enables or disables SFTP file sharing
SHARE_DISK_GROUP: disksharegroup  # Group name for sftp access to ext drive
SHARE_DISK_USER: diskshareuser  # User name for sftp access to an ext drive
SHARE_PUBLIC_USER: publicshareuser  # User name for sftp access to public dir on ext drive
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
