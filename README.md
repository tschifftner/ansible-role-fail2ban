# Ansible Role: Install Fail2Ban

[![Build Status](https://travis-ci.org/tschifftner/ansible-role-fail2ban.svg)](https://travis-ci.org/tschifftner/ansible-role-fail2ban)

Installs Fail2Ban from source on Debian/Ubuntu linux servers.

## Requirements

None

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```
fail2ban_download_url: 'https://github.com/fail2ban/fail2ban/archive/0.9.3.tar.gz'
fail2ban_workspace: '/opt'

fail2ban_jail_dir: '/etc/fail2ban/jail.d'

fail2ban_apt_packages:
  - whois
  - iptables-persistent
```

## Dependencies

None.

## Installation

```
$ ansible-galaxy install tschifftner.fail2ban
```

## Example Playbook

    - hosts: server
    
      vars:
        # Ignore all own ips
        fail2ban_ignoreip: "{{ ansible_all_ipv4_addresses }}"
          
        fail2ban_jails:
          - name: 'ssh'
            enabled: true
            port: ssh
            filter: sshd
            logpath: /var/log/auth.log
            maxretry: 3
        
          - name: 'ssh-ddos'
            enabled: true
            port: ssh
            bantime: 86400
            filter: 'sshd-ddos'
            logpath: /var/log/auth.log
            maxretry: 6

      roles:
        - { role: tschifftner.fail2ban }

## Supported OS
Ansible          | Debian Jessie    | Ubuntu 14.04
:--------------: | :--------------: | :-------------:
2.1              | Yes              | Yes

## License

MIT / BSD

## Author Information

 - [Tobias Schifftner](https://twitter.com/tschifftner), [ambimax® GmbH](https://www.ambimax.de)