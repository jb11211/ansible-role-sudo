# Sudo

[![Ansible Galaxy](http://img.shields.io/badge/galaxy-GROG.sudo-660198.svg?style=flat)](https://galaxy.ansible.com/list#/roles/4765)
[![Build Status](https://travis-ci.org/GROG/ansible-role-sudo.svg?branch=master)](https://travis-ci.org/GROG/ansible-role-sudo)

A role for managing sudo.

## Requirements

- Hosts should be bootstrapped for ansible usage (have python,...)
- Root privileges, eg `become: yes`
- Sudo should be available

## Role Variables

| Variable | Description | Default value |
|----------|-------------|---------------|
| `sudo_list` | List of users and their sudo settings **(see details!)** | `[]` |
| `sudo_list_host`| List of users and their sudo settings **(see details!)**  | `[]` |
| `sudo_list_group` | List of users and their sudo settings **(see details!)** | `[]` |
| `sudo_defaults` | List of defaults | `[]` |
| `sudo_host_aliases` | List of host aliases **(see details!)** | `[]` |
| `sudo_user_aliases` | List of user aliases **(see details!)** | `[]` |
| `sudo_runas_aliases` | List of run as aliases **(see details!)** | `[]` |
| `sudo_cmnd_aliases` | List of command aliases **(see details!)** | `[]` |
| `sudo_sudoersd` | Use sudoersd ? | `yes` |
| `sudo_sudoersd_dir` | Sudoersd directory | '/etc/sudoers.d' |

#### `sudo_list` details

`sudo_list`, `sudo_list_host` and `sudo_list_group` are merged when managing
the sudo settings. You can use the host and group lists to specify users
settings per host or group off hosts.

The sudo list allows you to define which users sudo settings must be managed.
Each item in the list can have following attributes:

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `hosts` | Hosts | yes | / |
| `as` | Operators | yes | / |
| `commands` | Commands | yes | / |
| `nopasswd` | No password sudo? | no | `no` |

###### Example `sudo_list`

```yaml
sudo_list:
  - name: root
    sudo:
      - hosts: ALL
      - as: ALL
      - commands: ALL
  - name: user1
  - name: user2
    sudo:
      - hosts: ALL
      - as: ALL
      - commands: ALL
      - nopasswd: yes
```

#### `sudo_***_aliases` details

The aliases lists allow you to specify multiple aliases. Each item in the
list has a name and an alias.

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `name` | Name of the alias | yes | / |
| `alias` | Alias | yes | / |

###### Example `sudo_***_aliases`

```yaml
sudo_***_aliases:
  - name: EXAMPLE1
    alias: 'shutdown'
  - name: EXPAMPLE2
    alias: 'test, test1, test2'
```

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: servers
  roles:
  - { role: GROG.sudo, become: yes }
```

Inside `group_vars/servers.yml`:

```yaml
sudo_list_group:
  - name: user
    sudo:
      - hosts: ALL
      - as: ALL
      - commands: ALL
```

## License

LGPLv3

## Contributing

All assistance, changes or ideas [welcome](https://github.com/GROG/ansible-role-sudo/issues)!

## Author Information

By [G. Roggemans](https://github.com/groggemans)
