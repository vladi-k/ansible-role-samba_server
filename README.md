ansible-role-samba_server
=========

Install and configure Samba server.

Requirements
------------

RHEL8 or above


Role Variables
--------------

* `samba_server_packages` - list of packages to install
* `samba_server_empty_conf` - boolean to empty smb.conf
* `samba_server_empty_conf_header` - header to set on top of smb.conf when emptied
* `samba_server_smb_conf` - list to configure smb.conf, example:

```yaml
samba_server_smb_conf:
  - section: global
    options:
      - option: server string
        value: "{{ ansible_hostname }}"
      - option: logging
        value: syslog
      - option: security
        value: user
      - option: passdb backend
        value: tdbsam
      - option: load printers
        value: "no"
      - option: printing
        value: bsd
      - option: printcap name
        value: /dev/null
      - option: disable spoolss
        value: "yes"
  - section: homes
    options:
      - option: comment
        value: Home Directories
      - option: browseable
        value: "no"
      - option: read only
        value: "no"
      - option: valid users
        value: "%S"
```

* `samba_server_services` - list of samba systemd services
* `samba_server_users` - list of samba users, example:

```yaml
samba_server_users:
  - name: myuser
    password: verysecure
```

Dependencies
------------

Collections:

* `ansible.builtin`
* `community.general`

Roles:

* [ansible-role-selinux](https://github.com/vladi-k/ansible-role-selinux) (or similar) if SELinux is in enforcing mode.

Example Playbook
----------------

```
- hosts: servers
  roles:
    - ansible-role-samba_server
```

License
-------

GPLv3

Author Information
------------------

Vladimir Vasilev (@vladi-k)
