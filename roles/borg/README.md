Role Name
=========

Install and config Borg and Borgmatic backup solution.

Role Variables
--------------

```yml
# Base vars
DISK_LABEL: disk  # Label of the disk from which data is backed up

# Borg vars
BORG_TYPE: server  # Role of this machine in backup process (server or client)
BORG_SERVER_GROUP: backup_server  # Ansible inventory group for backup servers
BORG_CLIENT_GROUP: master_server  # Ansible inventory group for servers to be backed up
BORG_USER: borg  # User under which Borg backup will run
BORG_DISK_LABEL: BORG_BACKUP_DISK  # Label of the disk where Borg repository will be stored
BORG_BACKUP_PATH: /mnt/{{ BORG_DISK_LABEL }}/borg  # Path to the Borg backup repository
BORG_SSH_PRIVATE_KEY_NAME: borg_ssh.pem  # Name of the Borg SSH private key file
BORG_SSH_PUBLIC_KEY_NAME: '{{ BORG_SSH_PRIVATE_KEY_NAME }}.pub'  # Name of the Borg SSH public key file

# Borgmatic config vars
BORGMATIC_BACKUP_FREQUENCY: 00:00  # Frequency of backups in cron format
BORGMATIC_ENCRYPTION_PASS: qwerty1234!  # Password for encrypting Borg backups
BORGMATIC_COMPRESSION: zlib  # Compression algorithm to be used by Borg
BORGMATIC_KEEP_DAILY: 7  # Number of daily backups to keep
BORGMATIC_KEEP_WEEKLY: 4  # Number of weekly backups to keep
BORGMATIC_KEEP_MOUNTHLY: 6  # Number of monthly backups to keep
BORGMATIC_KEEP_YEARLY: 1  # Number of yearly backups to keep

BORGMATIC_BACKUP_SOURCES:  # List of directories to backup
  - /mnt/{{ DISK_LABEL }}/backup
```

Example Playbook
----------------

```yml
  - hosts: backup_server
    roles:
       - role: borg
```

License
-------

GPL

Author Information
------------------

[Grell Gragham](https://github.com/ggragham)
