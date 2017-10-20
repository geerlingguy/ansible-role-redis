# Ansible Role: Redis

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-redis.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-redis)

Installs [Redis](http://redis.io/) on RHEL/CentOS or Debian/Ubuntu.

## Requirements

On RedHat-based distributions, requires the EPEL repository (you can simply add the role `geerlingguy.repo-epel` to install ensure EPEL is available).

## Role Variables

    redis_enablerepo: epel

(Used only on RHEL/CentOS) The repository to use for Redis installation.

Available variables are listed below, along with default values (see `defaults/main.yml`):

    redis_port: 6379
    redis_bind_interface: 127.0.0.1

Port and interface on which Redis will listen. Set the interface to `0.0.0.0` to listen on all interfaces.

    redis_unixsocket: ''

If set, Redis will also listen on a local Unix socket.

    redis_timeout: 300

Close a connection after a client is idle `N` seconds. Set to `0` to disable timeout.

    redis_loglevel: "notice"
    redis_logfile: /var/log/redis/redis-server.log

Log level and log location (valid levels are `debug`, `verbose`, `notice`, and `warning`).

    redis_databases: 16

The number of Redis databases.

    # Set to an empty set to disable persistence (saving the DB to disk).
    redis_save:
      - 900 1
      - 300 10
      - 60 10000

Snapshotting configuration; setting values in this list will save the database to disk if the given number of seconds (e.g. `900`) and the given number of write operations (e.g. `1`) have occurred.

    redis_rdbcompression: "yes"
    redis_dbfilename: dump.rdb
    redis_dbdir: /var/lib/redis

Database compression and location configuration.

    redis_maxmemory: 0

Limit memory usage to the specified amount of bytes. Leave at 0 for unlimited.

    redis_maxmemory_policy: "noeviction"

The method to use to keep memory usage below the limit, if specified. See [Using Redis as an LRU cache](http://redis.io/topics/lru-cache).

    redis_maxmemory_samples: 5

Number of samples to use to approximate LRU. See [Using Redis as an LRU cache](http://redis.io/topics/lru-cache).

    redis_appendonly: "no"

The appendonly option, if enabled, affords better data durability guarantees, at the cost of slightly slower performance.

    redis_appendfsync: "everysec"

Valid values are `always` (slower, safest), `everysec` (happy medium), or `no` (let the filesystem flush data when it wants, most risky).

    # Add extra include files for local configuration/overrides.
    redis_includes: []

Add extra include file paths to this list to include more/localized Redis configuration.

    redis_requirepass: ""

Set a password to require authentication to Redis. You can generate a strong password using `echo "my_password_here" | sha256sum`.

    redis_disabled_commands: []

For extra security, you can disable certain Redis commands (this is especially important if Redis is publicly accessible). For example:

    redis_disabled_commands:
      - FLUSHDB
      - FLUSHALL
      - KEYS
      - PEXPIRE
      - DEL
      - CONFIG
      - SHUTDOWN

Redis systemd overrides below.  This allows for more flexibility in installing more than one instance, such as a master/slave configuration on a single server.

    redis_daemon: "redis"

The redis daemon name name used for creating the config file and mapping to the service.  Changing this for multiple instances will allow for different config files to be created, mapping to the systemd service file for management.

    redis_svc_user: "redis"
    redis_svc_group: "redis"

The user and group that will own the service while it is running.

### Best Practices
Some default configurable best practices per redis.io that can be found here [Redis Administration](https://redis.io/topics/admin)

    vm_overcommit_mem: True

The kernel will not overcommit memory which allows for more flexibility for memory but also increases risk of memory overload. Consider maxmemory settings and system swap as well.

    disable_transparent_hugepage: True

Transparent hugepages are often enabled by default.  Redis will warn of this if enabled.  Enabling them may cause delays allocating memory during runtime, so it is recommended to disable them by default.


## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - { role: geerlingguy.redis }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/).
