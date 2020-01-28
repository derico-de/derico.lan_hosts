# derico.lan_hosts

Ansible role to configure lan hosts in /etc/hosts with a template and blockinline.

## Minimum Ansible Version:

2.9

## Supported versions and systems

| System / Odoo       | 12.0 | 13.0 |
|---------------------|------|------|
| Debian 10 (buster)  | yes  | yes  |

## Usage

### Play

```yaml
  - hosts: virtual_servers #all_machines
    become: True

    roles:
      - role: derico.lan_hosts
        vars:
          lan_hosts: "{{ groups['virtual_servers'] }}"
```

### Inventory

```
mail ansible_ssh_host=xxx.xxx.xxx.xxx lan_ip=10.0.0.10
db ansible_ssh_host=xxx.xxx.xxx.xxx lan_ip=10.0.0.20
web1 ansible_ssh_host=xxx.xxx.xxx.xxx lan_ip=10.0.0.30
web2 ansible_ssh_host=xxx.xxx.xxx.xxx lan_ip=10.0.0.31
web3 ansible_ssh_host=xxx.xxx.xxx.xxx lan_ip=10.0.0.32
```

### Result

/etc/hosts example:

```
127.0.0.1	localhost
xxx.xxx.xxx.xxx derico.de

### BEGIN ANSIBLE MANAGED BLOCK ###

10.0.0.10     mail.lan
10.0.0.20     db.lan
10.0.0.30     web1.lan
10.0.0.31     web2.lan
10.0.0.31     web3.lan

### END ANSIBLE MANAGED BLOCK ###
```