Docker role
=========

Install and config Docker.

Role Variables
--------------

```yml
DOCKER_NETWORK_NAME: homelab_network  # Name of the Docker network.
DOCKER_BRIDGE_NAME: homelab_bridge  # Name of the bridge interface for the Docker network.
```

Example Playbook
----------------

```yml
  - hosts: servers
    roles:
       - role: docker
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
