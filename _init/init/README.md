Init role
=========

Add ssh key. Configure ssh. Disable root. Set passwordless sudo.

Role Variables
--------------

```yml
USERNAME: '{{ ansible_user }}' # Username of the main user on the server. Taken from inventory.
SSH_KEY_PATH: ./assets/srv_key.pem.pub # Path to public ssh key.
SSH_PORT: 22 # Port set for ssh.
```

Example Playbook
----------------

```yml
  - hosts: servers
    roles:
      - role: init
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
