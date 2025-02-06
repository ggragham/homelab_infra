Base role
=========

Apply firewall rules, install and config VPN Client, config File Sharing, etc

Role Variables
--------------

```yml
DOMAIN_NAME: example.com  # Domain name for server.
NETWORK_INTERFACE: eth0  # Network interface to be used.

# SSH
SSH_PORT: 22  # Set ssh port for firewall.
SERVER_SUBNET: 192.168.1.0/24  # Server subnet for network configuration.

# External Disk
EXT_DISK_ENABLED: true  # Enables or disables external disk mounting.
DISK_LABEL: disk  # External disk label.
DISK_ENCRYPTED: false  # Disk encryption status.
DISK_KEYFILE: keyfile.pem  # Encryption key file name.
DISK_KEYFILE_PATH: '{{ ASSETS_PATH }}/{{ DISK_KEYFILE }}'  # Path to encryption key file.
DISK_FSTYPE: btrfs  # Disk filesystem type.
DISK_PATH: /mnt/{{ DISK_LABEL }}  # Disk mount path.
DISK_DATA_PATH: '{{ DISK_PATH }}/data'  # Data path.
DISK_DATABASE_PATH: '{{ DISK_PATH }}/database'  # Database path on external disk.

DISK_SUBVOLS:  # List of BTRFS subvolumes
  - name: storage
    subvol: '@storage'  # Subvolume name in filesystem
    path: '{{ DISK_DATA_PATH }}'  # Subvolume mount point
    compression: zstd:1  # Subvolume compression

  - name: db
    subvol: '@db'
    path: '{{ DISK_DATABASE_PATH }}'
    compression: zstd:1

# SFTP
SFTP_ENABLE: false  # Enable or disable SFTP access.
SHARE_DISK_GROUP: disksharegroup  # Group name for sftp access to ext drive
SHARE_DISK_USER: diskshareuser  # User name for sftp access to an ext drive
SHARE_PUBLIC_USER: publicshareuser  # User name for sftp access to public dir on ext drive

# WireGuard
WIREGUARD_ENABLED: false  # Enable or disable WireGuard VPN.
WIREGUARD_CONFIG_PATH_SRC: '{{ ASSETS_PATH }}/wg0.conf'  # Source path for WireGuard configuration.
WIREGUARD_PORT: 51820  # Port for WireGuard VPN.
WIREGUARD_SUBNET: 10.8.0.0/24  # Subnet for WireGuard VPN.

## OpenVPN
OPENVPN_ENABLED: false  # Enable or disable OpenVPN.
OPENVPN_CONFIG_PATH: '{{ ASSETS_PATH }}/client.ovpn'  # Path to OpenVPN configuration file.
OPENVPN_PORT: 1194  # Port for OpenVPN.
VPN_SUBNET: 10.8.0.0/24  # Subnet for OpenVPN VPN.
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
