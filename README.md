haproxy
=======

Installs and configures HAProxy

Requirements
------------

This role requires Ansible 1.6 or higher.

Role Variables
--------------

| Name                             | Default    | Description                                                          |
|----------------------------------|------------|----------------------------------------------------------------------|
| haproxy_version                  | 1.5.14     | Version of HAProxy to install                                        |
| haproxy_defaults_mode            | http       | Running mode or protocol of the instance                             |
| haproxy_defaults_timeout_connect | 5000       | Maximum time to wait for a connection attempt to a server to succeed |
| haproxy_defaults_timeout_client  | 50000      | Maximum inactivity time on the client side                           |
| haproxy_defaults_timeout_server  | 50000      | Maximum inactivity time on the server side                           |

Dependencies
------------

None

Example Playbook
----------------

Install HAProxy
```
- hosts: all
  roles:
    - { role: kbrebanov.haproxy }
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
