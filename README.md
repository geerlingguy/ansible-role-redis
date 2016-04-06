# Ansible Role: Redis

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-redis.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-redis)

Installs [Redis](http://redis.io/) on RHEL/CentOS or Debian/Ubuntu.

## Requirements

On RedHat-based distributions, requires the EPEL repository (you can simply add the role `geerlingguy.repo-epel` to install ensure EPEL is available).

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

    redis_sysctl_overcommit_memory: 1

Sysctl vm.overcommit_memory key, required for safe data dumping to disk.

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

    redis_requirepass: false

If set, connected clients will have to authenticate with specified password. 


    redis_slave: false

Master-Slave replication. If set, Redis serves as slave instance in cluster.

    redis_master_ip: 127.0.0.1
    redis_master_port: 6379

Master server parameters.

    redis_masterauth: false

Master server password(which set with "requirepass" configuration directive ).

    redis_slave_serve_stale_data: "yes"

If set to "yes", slave will serve requests while not in sync state. If set "no" slave will reply with "SYNC with master in progress" message.

    redis_slave_read_only: "yes"

Set slave read-only.

    redis_includes: []

Add extra include file paths to this list to include more/localized Redis configuration.

    redis_extra_params: {}

Add extra redis.conf parameters which don't have dedicated role variables. Example usage:

    redis_extra_prams:
      repl-diskless-sync: "no"
      repl-diskless-sync_delay: 5
      repl-ping-slave-period: 10
      repl-timeout: 60

####Redis Sentinel related variables

    redis_sentinel_enabled: false

Enable Redis Sentinel for automatic failover procedure.

    redis_sentinel_dir: /tmp
    redis_sentinel_port: 26379
    redis_sentinel_logfile: /var/log/redis/sentinel.log

Redis Sentinel general parameters.

    redis_sentinel_monitors:
      - name: mymaster
        host: 127.0.0.1
        port: 6379
        quorum: 2
        options: 
          auth-pass: false
          down-after-milliseconds: 30000
          parallel-syncs: 1
          failover-timeout: 180000
          notification-script: false
          client-reconfig-script: false

Configuration for specific master server. See http://redis.io/topics/sentinel for details

    redis_sentinel_extra_params: {}

Add extra sentinel parameters which don't have dedicated role variables. Use the same way as for redis_extra_params

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
