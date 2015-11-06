haproxy
=======

[![Ansible Role](https://img.shields.io/ansible/role/5700.svg)](https://galaxy.ansible.com/list#/roles/5700)

Installs and configures HAProxy

Requirements
------------

This role requires Ansible 1.8 or higher.

Role Variables
--------------

| Name                                    | Default                                                                                                                                                                  | Description                                                                                                               |
|-----------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| haproxy_version                         | 1.6                                                                                                                                                                      | Version of HAProxy to install                                                                                             |
| haproxy_global_daemon                   | true                                                                                                                                                                     | Makes the process fork in the background                                                                                  |
| haproxy_global_log                      | [{address: /dev/log, length: '', facility: local0, level: ''}, {address: /dev/log, length: '', facility: local1, level: notice }]                                        | Configures global syslog servers                                                                                          |
| haproxy_global_maxconn                  | 2000                                                                                                                                                                     | Sets the global maximum per-process number of concurrent connections                                                      |
| haproxy_global_ssl_default_bind_ciphers | ["ECDH+AESGCM", "DH+AESGCM", "ECDH+AES256", "DH+AES256", "ECDH+AES128", "DH+AES", "ECDH+3DES", "DH+3DES", "RSA+AESGCM", "RSA+AES", "RSA+3DES", "!aNULL", "!MD5", "!DSS"] | Sets the default cipher algorithms ("cipher suite") that are negotiated during the SSL/TLS handshake for all "bind" lines |
| haproxy_global_ssl_default_bind_options | ["no-sslv3"]                                                                                                                                                             | Sets default SSL options to force on all "bind" lines                                                                     |
| haproxy_global_stats_timeout            | 10s (Ubuntu: 30s)                                                                                                                                                        | The default timeout on the stats socket                                                                                   |
| haproxy_defaults_log                    | global                                                                                                                                                                   | Default logging                                                                                                           |
| haproxy_defaults_mode                   | http                                                                                                                                                                     | Running mode or protocol of the instance                                                                                  |
| haproxy_defaults_option_dontlognull     | true                                                                                                                                                                     | Enable or disable logging of null connections                                                                             |
| haproxy_defaults_option_httplog         | true                                                                                                                                                                     | Enable logging of HTTP request, session state and timers                                                                  |
| haproxy_defaults_option_httplog_clf     | false                                                                                                                                                                    | If enabled, then the output format will be the CLF format instead of HAProxy's default HTTP format                        |
| haproxy_defaults_timeout_connect        | 5000                                                                                                                                                                     | Maximum time to wait for a connection attempt to a server to succeed                                                      |
| haproxy_defaults_timeout_client         | 50000                                                                                                                                                                    | Maximum inactivity time on the client side                                                                                |
| haproxy_defaults_timeout_server         | 50000                                                                                                                                                                    | Maximum inactivity time on the server side                                                                                |
| haproxy_listen_section                  | false                                                                                                                                                                    | Enable or disable listen proxy section                                                                                    |
| haproxy_listen_name                     | ''                                                                                                                                                                       | Sets name of listen proxy                                                                                                 |
| haproxy_listen_bind                     | ''                                                                                                                                                                       | Sets listen bind address                                                                                                  |
| haproxy_listen_balance_algorithm        | ''                                                                                                                                                                       | Sets listen balance algorithm                                                                                             |
| haproxy_listen_balance_arguments        | ''                                                                                                                                                                       | Sets listen balance arguments                                                                                             |
| haproxy_listen_mode                     | ''                                                                                                                                                                       | Sets listen mode                                                                                                          |
| haproxy_listen_log                      | ''                                                                                                                                                                       | Sets listen log                                                                                                           |
| haproxy_listen_servers                  | []                                                                                                                                                                       | Configures listen servers                                                                                                 |

Dependencies
------------

None

Example Playbook
----------------

Install HAProxy
```
- hosts: all
  roles:
    - kbrebanov.haproxy
```

Install older version of HAProxy
```
- hosts: all
  vars:
    haproxy_version: 1.5.14
  roles:
    - kbrebanov.haproxy
```

Install HAProxy and configure listen proxy section
```
- hosts: all
  vars:
    haproxy_listen_section: true
    haproxy_listen_name: "http-in"
    haproxy_listen_bind: "0.0.0.0:80"
    haproxy_listen_mode: "tcp"
    haproxy_listen_balance_algorithm: "roundrobin"
    haproxy_listen_log: "global"
    haproxy_listen_servers:
      - name: "server1"
        address: "192.168.1.1:8080"
      - name: "server2"
        address: "172.16.32.44:9090"
  roles:
    - kbrebanov.haproxy
```

License
-------

BSD

Author Information
------------------

Kevin Brebanov
