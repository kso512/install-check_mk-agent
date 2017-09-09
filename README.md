[![Build Status](https://travis-ci.org/kso512/install-check_mk-client.svg?branch=master)](https://travis-ci.org/kso512/install-check_mk-client)

# [install-check_mk-client](https://galaxy.ansible.com/kso512/install-check_mk-client/)

An [Ansible](https://www.ansible.com/) [Role](http://docs.ansible.com/ansible/playbooks_roles.html#roles) to install the agent/client for [Check_MK RAW](http://mathias-kettner.com/check_mk_introduction.html).

This role utilizes SSH on Unix-type systems instead of the default port 6556.  This encrypts communications and avoids opening a new port for monitoring and setting up a new service.

Tested with [Travis continuous integration](https://travis-ci.org/) on the following distributions:

- [CentOS-6](https://wiki.centos.org/Manuals/ReleaseNotes/CentOS6.9)
- [CentOS-7](https://wiki.centos.org/Manuals/ReleaseNotes/CentOS7)
- [Debian 8 "Jessie"](https://www.debian.org/releases/jessie/)
- [Debian 9 "Stretch"](https://www.debian.org/releases/stretch/)
- [Ubuntu 12.04 LTS "Precise Pangolin"](http://releases.ubuntu.com/precise)
- [Ubuntu 14.04 LTS "Trusty Tahr"](http://releases.ubuntu.com/trusty/)
- [Ubuntu 16.04 LTS "Xenial Xerus"](http://releases.ubuntu.com/xenial/)

The following operating systems are also supported and tested manually:

- [FreeBSD 10.3](https://www.freebsd.org/releases/10.3R/relnotes.html)
- [FreeBSD 11.0](https://www.freebsd.org/releases/11.0R/relnotes.html)
- [Microsoft Windows](https://www.microsoft.com/en-us/windows/)
- [openSUSE 13.2](https://en.opensuse.org/Portal:13.2)

## Requirements

If the server is Windows and has a firewall enabled, it may need to be altered to allow incoming packets on TCP port 6556.

## Role Variables

### Defaults

| Variable | Description | Value |
| -------- | ----------- | ----- |
| install_check_mk_client_prereqs | List of packages to install before configuring agent | `sudo` |
| install_check_mk_client_user | Name of user to configure | `cmkagent` |
| install_check_mk_client_home | Home folder of configured user | `"/home/{{ install_check_mk_client_user }}"` |
| install_check_mk_client_count_users_warn | Logged in users, warning threshold | `10` |
| install_check_mk_client_count_users_crit | Logged in users, critical threshold | `15` |
| install_check_mk_client_count_zombie_procs_warn | Zombie processes, warning threshold | `5` |
| install_check_mk_client_count_zombie_procs_crit | Zombie processes, critical threshold | `10` |
| install_check_mk_client_freebsd_plugins | List of active FreeBSD plugins | `[]` |
| install_check_mk_client_local_checks | List of active local checks | `count_users`, `count_zombie_procs` |
| install_check_mk_client_plugins | List of active plugins | ` mk_inventory`, `lvm`, `smart` |
| install_check_mk_client_win_tmp | Temporary location of Windows installation file | `c:\check_mk_agent.msi` |
| install_check_mk_client_win_filename | Filename of Windows installation file | `check_mk_agent.msi` |
| install_check_mk_client_win_config | Filename of Windows configuration template | `check_mk.ini.j2` |
| install_check_mk_client_win_folder | Folder the agent gets installed to | `C:\Program Files (x86)\check_mk\` |
| install_check_mk_client_win_plugins | List of active Windows plugins | `mk_inventory.vbs` |

## Dependencies

This role depends on no other roles.

## Example Playbook

Complete example:

    - hosts: all
      roles:
         - { role: install-check_mk-client, install_check_mk_client_user: agent }

## License

BSD

## Author Information

> Chris Lindbergh

