Jellyfin Role
=============

Install and configure Jellyfin to Proxmox LXC with hardware acceleration (AMD GPU only).

Requirements
------------

- AMD GPU hardware.
- Proxmox VE host with an available LXC container (Debian/Ubuntu based).
- Python packages on the control node:
  * `proxmoxer` >= 2.0
  * `requests`

Example install:
```bash
python3 -m pip install --user "proxmoxer>=2.0" requests
```

Role Variables
--------------

```yml
PROXMOX_HOSTNAME: example.com  # Proxmox VE instance hostname.
PROXMOX_NODE: srv-01  # Proxmox node name where the container runs.
PROXMOX_API_HOST: pve.example.com  # Proxmox API hostname or IP.
PROXMOX_API_PORT: 8006  # Proxmox API port.
PROXMOX_API_USER: root@pam  # Proxmox API username.
PROXMOX_API_PASSWORD: foobar123  # Proxmox API password.
PROXMOX_CONTAINER_VMID: '100'  # Numeric VMID of the LXC container.
PROXMOX_VALIDATE_SSL: false  # Whether to verify the API TLS certificate.

PROXMOX_MOUNT_VOLUMES:  # Bind mounts from host into the container.
  - id: mp0  # LXC mount slot.
    host_path: /opt/media  # Absolute path on the Proxmox node.
    mountpoint: /mnt/media  # Target path inside the container.
  - id: mp1
    host_path: /opt/data
    mountpoint: /mnt/data
```

Optional Variables
------------------

### Force Run Install
Run the Jellyfin install script even if the package is already installed.

```bash
ansible-playbook <playbook_name>.yml --tags jellyfin \
    -e jellyfin_force_run_install=true
```

Example Playbook
----------------

```yml
  - hosts: pve-lxc-01
    roles:
       - role: jellyfin
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
