# Ansible Role: Redis

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-redis.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-redis)

Installs [Redis](http://redis.io/) on RHEL/CentOS or Debian/Ubuntu.

## Requirements

On RedHat-based distributions, requires the EPEL repository (you can simply add the role `geerlingguy.repo-epel` to install ensure EPEL is available).

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    redis_port: 6379
    redis_bind_interface: 127.0.0.1
    redis_unixsocket: ''
    redis_timeout: 300

    redis_loglevel: "notice"
    redis_logfile: /var/log/redis/redis-server.log

    redis_databases: 16

    # Set to an empty set to disable persistence (saving the DB to disk).
    redis_save:
      - 900 1
      - 300 10
      - 60 10000

    redis_rdbcompression: "yes"
    redis_dbfilename: dump.rdb
    redis_dbdir: /var/lib/redis

    redis_appendonly: "no"
    redis_appendfsync: "everysec"

    redis_vm_enabled: "no"

    # Add extra include files for local configuration/overrides.
    redis_includes: []

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - { role: geerlingguy.redis }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](http://jeffgeerling.com/), author of [Ansible for DevOps](http://ansiblefordevops.com/).
