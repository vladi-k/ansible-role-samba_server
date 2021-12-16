ansible-role-samba_server
=========

Install and configure Samba server.

Requirements
------------

RHEL8 or above


Role Variables
--------------

* `samba_server_packages` - list of packages to install
* `samba_server_trunc_conf` - boolean to truncate smb.conf
* `samba_server_trunc_header` - header to set on top of smb.conf when truncated
* `samba_server_workground` - workgroup name
* `samba_server_conf_global` - configures [global] section in smb.conf
* `samba_server_homes_enabled` - boolean to enable [homes] shares in smb.conf
* `samba_server_conf_homes_valid_users` - list of valid users for home shares
* `samba_server_conf_homes` - configures [homes] section in smb.conf
* `samba_server_conf_shares` - list of shares in smb.conf, example:

```yaml
samba_server_conf_shares:
  - section: movies
    options:
      - option: path
        value: /mnt/movies
      - option: browsable
        value: 'Yes'
      - option: guest ok
        value: 'Yes'
      - option: read only
        value: 'Yes'
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

If SELinux is in enforcing mode you need another role to set proper context

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

Vladimir Vasilev
