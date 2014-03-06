# Ansible Role: Redis

Installs Redis on RHEL/CentOS 6.x.

## Requirements

None.

## Role Variables

Available variables are listed below, along with default values (see `vars/main.yml`):

    TODO

## Dependencies

  - geerlingguy.repo-epel

## Example Playbook

    - hosts: all
      vars_files:
        - vars/main.yml
      roles:
        - { role: geerlingguy.redis }

*Inside `vars/main.yml`*:

    TODO

## License

MIT / BSD

## Author Information

This role was created in 2014 by Jeff Geerling (@geerlingguy), author of Ansible for DevOps. You can find out more about the book at http://ansiblefordevops.com/, and learn about the author at http://jeffgeerling.com/.
