# [install-check_mk-agent](https://galaxy.ansible.com/kso512/install-check_mk-agent/)

![Ansible Role](https://img.shields.io/ansible/role/d/16931) [![made-with-bash](https://img.shields.io/badge/Made%20with-Bash-1f425f.svg)](https://www.gnu.org/software/bash/) [![made-with-Markdown](https://img.shields.io/badge/Made%20with-Markdown-1f425f.svg)](http://commonmark.org) ![GitHub](https://img.shields.io/github/license/kso512/install-check_mk-agent)

[![GitHub release (latest SemVer)](https://img.shields.io/github/v/release/kso512/install-check_mk-agent)](https://github.com/kso512/install-check_mk-agent) ![GitHub Release Date](https://img.shields.io/github/release-date/kso512/install-check_mk-agent) ![GitHub repo size](https://img.shields.io/github/repo-size/kso512/install-check_mk-agent) ![GitHub issues](https://img.shields.io/github/issues-raw/kso512/install-check_mk-agent) [![GitHub forks](https://img.shields.io/github/forks/Naereen/StrapDown.js.svg?style=social&label=Fork&maxAge=2592000)](https://GitHub.com/Naereen/StrapDown.js/network/)

An [Ansible](https://www.ansible.com/) [Role](http://docs.ansible.com/ansible/playbooks_roles.html#roles) to install the agent/client for [Check_MK RAW](http://mathias-kettner.com/check_mk_introduction.html).

All tasks are tagged with `install-check-mk-agent`.

This role utilizes SSH on Unix-type systems instead of the default port 6556.  This encrypts communications and avoids opening a new port for monitoring and setting up a new service.

Tested manually with the [Ansible Role Test Shim Script from Jeff Geerling](https://gist.github.com/geerlingguy/73ef1e5ee45d8694570f334be385e181) on the following distributions:

- [CentOS-7](https://wiki.centos.org/Manuals/ReleaseNotes/CentOS7)
- [CentOS-8](https://wiki.centos.org/Manuals/ReleaseNotes/CentOSLinux8)
- [Debian 9 "Stretch"](https://www.debian.org/releases/stretch/)
- [Debian 10 "Buster"](https://www.debian.org/releases/buster/)
- [Ubuntu 18.04 LTS "Bionic Beaver"](https://releases.ubuntu.com/bionic/)
- [Ubuntu 20.04 LTS "Focal Fossa"](https://releases.ubuntu.com/focal/)

The following operating systems are also supported and tested manually:

- [FreeBSD 10.3](https://www.freebsd.org/releases/10.3R/relnotes.html)
- [FreeBSD 11.0](https://www.freebsd.org/releases/11.0R/relnotes.html)
- [Microsoft Windows](https://www.microsoft.com/en-us/windows/)
- [openSUSE 13.2](https://en.opensuse.org/Portal:13.2)

## Requirements

Requirements on host that executes role:

- groupadd
- groupdel
- groupmod

Requirements on host that executes role with APT:

- python-apt (python 2)
- python3-apt (python 3)
- aptitude (before 2.4)

Requirements on host that executes role with YUM:

- yum

If the server is Windows and has a firewall enabled, it may need to be altered to allow incoming packets on TCP port 6556.

## Role Variables

### Defaults

| Variable | Description | Value |
| -------- | ----------- | ----- |
| install_check_mk_agent_prereqs | List of packages to install before configuring agent | `sudo` |
| install_check_mk_agent_user | Name of user to configure | `cmkagent` |
| install_check_mk_agent_home | Home folder of configured user | `"/home/{{ install_check_mk_agent_user }}"` |
| install_check_mk_agent_count_users_warn | Logged in users, warning threshold | `10` |
| install_check_mk_agent_count_users_crit | Logged in users, critical threshold | `15` |
| install_check_mk_agent_count_zombie_procs_warn | Zombie processes, warning threshold | `5` |
| install_check_mk_agent_count_zombie_procs_crit | Zombie processes, critical threshold | `10` |
| install_check_mk_agent_freebsd_plugins | List of active FreeBSD plugins | `[]` |
| install_check_mk_agent_local_checks | List of active local checks | `count_users`, `count_zombie_procs` |
| install_check_mk_agent_plugins | List of active Linux plugins | See [NOTE A](https://github.com/kso512/install-check_mk-agent#note-a) |
| install_check_mk_agent_win_tmp | Temporary location of Windows installation file | `"c:\{{ install_check_mk_agent_win_filename }}"` |
| install_check_mk_agent_win_filename | Filename of Windows installation file | `check_mk_agent.msi` |
| install_check_mk_agent_win_config | Filename of Windows configuration template | `check_mk.example.ini.j2` |
| install_check_mk_agent_win_folder | Folder the agent gets installed to | `C:\Program Files (x86)\check_mk\` |
| install_check_mk_agent_win_plugins | List of active Windows plugins | `mk_inventory.vbs` |

### NOTE A

install_check_mk_agent_plugins:

- lvm
- mk_inventory.linux
- mk_iptables
- mk_nfsiostat
- mk_sshd_config
- netstat.linux
- nfsexports
- smart

## Dependencies

This role depends on none other.

## Example Playbook

Complete example:

    - hosts: all
      roles:
         - { role: install-check_mk-agent, install_check_mk_agent_user: agent }

## License

[GNU General Public License version 2](https://www.gnu.org/licenses/gpl-2.0.txt)

## Author Information

> Chris Lindbergh @kso512
