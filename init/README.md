Init role
=========

Add ssh key. Configure ssh. Disable root. Set passwordless sudo.

Role Variables
--------------

USERNAME - username of the main user on the server (Taken from inventory. "admin" by default)
SSH_KEY_PATH - path to public ssh key (./assets/srv_key.pem.pub by default)
SSH_PORT - port set for ssh (22 by default)

Example Playbook
----------------

    - hosts: servers
      roles:
        - role: init

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
