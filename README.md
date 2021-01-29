[![Ansible-Test](https://github.com/mediafellows/ansible-role-filebeat/workflows/Ansible-Test/badge.svg)](https://github.com/mediafellows/ansible-role-filebeat/actions?query=workflow%3AAnsible-Test)

# Ansible role to install & configure filebeat
Ansible role that installs filebeat on Linux using the apt package elastic provides.

Also sets up the filebeat.yml config file based on role parameters.
This role ist mostly designed to setup filebeat for collection of logfile content and sending 
it on to logstash. If you want other outputters you might have to change a bunch of things first!

## Requirements
Debian based Linux, tested on Ubuntu. Recent version of Ansible. Only utilized Ansible core modules.

## Role Variables

Role variables you can set or overwrite:

```yaml
# List of files to read logs from (aka inputs):
filebeat_prospectors:
  - { paths: /var/log/*/*.log, input_type: log, document_type: log}
# list of module packs for certain software/OS logs
filebeat_modules:
  - module: nginx
# Logstash server to send logs to (logstash output):
filebeat_logstash_server: 'logstash.server.com'
filebeat_logstash_server_port: 5044
filebeat_logstash_tls: false
filebeat_logstash_tls_certificate_authorities: []
filebeat_logstash_tls_certificate:
filebeat_logstash_tls_certificate_key:
filebeat_logstash_tls_insecure: false
```

You can also define variable `filebeat_extra_prospectors` on a per-host or
per-group basis.  This variable is concatenated with `filebeat_prospectors`
when rendering the configuration template.

## Dependencies
This role has no dependencies to other roles.

## Example Playbook
Copy this role into the roles/mediafellows.filebeat dir in your Ansible project. Preferably add it as a submodule.
You can also install it with `ansible-galaxy install mediafellows.filebeat`.
Then use it like so:

```yaml
- name: My nice play
  hosts: servers
  vars:
    - filebeat_logstash_server: 'logstash.my.server'
    - filebeat_logstash_server_port: 5044
    - filebeat_logfiles:
      - /var/log/syslog
  roles:
    - mediafellows.filebeat
```

## License
BSD

## Author Information
Stefan Horning <stefan.horning@mediafellows.com>
