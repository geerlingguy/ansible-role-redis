# Ansible Role: Redis

[![Build Status](https://travis-ci.org/geerlingguy/ansible-role-redis.svg?branch=master)](https://travis-ci.org/geerlingguy/ansible-role-redis)

Installs [Redis](http://redis.io/) on RHEL/CentOS or Debian/Ubuntu.

## Requirements

On RedHat-based distributions, requires the EPEL repository.

## Role Variables

None.

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
