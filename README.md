# Ansible Collection - crrlcx.bootstrap

[[_TOC_]]

## Description

  Ansible Collection: Bootstrap

  This collection provides a set of bootstrap roles designed for Debian-based systems,
  serving as a lightweight alternative to Cloud-init. It automates initial host
  provisioning and configuration tasks, enabling consistent and repeatable setup
  of Debian-based environments without relying on Cloud-init.

## Installation

Add to the `requirements.yml` of Ansible project

```yaml
---
# Ansible Galaxy collections
collections:
  - name: https://github.com/crrlcx/ansible-collection-boostrap
    type: git
```

Install with Ansible Galaxy CLI

```shell
ansible-galaxy install -r requirements.yml
```

## Collection roles usage example

```yaml
---
- hosts: all
  gather_facts: true
  become: true
  collections:
    - crrlcx.bootstrap
  roles:
    - role: crrlcx.bootstrap.sysctl
```

## Collection playbook usage example

Run playbook as is

```shell
ansible-playbook crrlcx.bootstrap.bootstrap
```

Import playbook from collection

```yaml
---
import_playbook: crrlcx.bootstrap.bootstrap
```

## Includes

- [ca](roles/ca) - set custom CA certificates trusted (system wide).
- [disk](roles/disk) - manage physical and logical volumes of block devices.
- [dns](roles/dns) - set DNS with systemd power.
- [grub](roles/grub) - manage GRUB bootloader configuration and kernel cmdline parameters.
- [hosts](roles/hosts) - manage hostname and /etc/hosts.
- [inadyn](roles/inadyn) - manage inadyn dynamic DNS client configuration and systemd service.
- [kmod](roles/kmod) - manage kernel module settings, initramfs modules, and modprobe options.
- [lvm](roles/lvm) - manage LVM physical and logical volumes.
- [motd](roles/motd) - manage MOTD and issue banners via fastfetch with cron.hourly.
- [ntp](roles/ntp) - set timezone and sync time with systemd power.
- [repositories](roles/repositories) - manage system package manager repositories.
- [ssh](roles/ssh) - secure ssh-client and ssh-server configuration (hardening), exported from `dev-sec/ansible-collection-hardening`.
- [swap](roles/swap) - install and configure zSwap and zRAM as systemd service.
- [sysctl](roles/sysctl) - manage system and kernel options with sysctl.
- [udev](roles/udev) - manage block and network devices with udev rules.

## More information about collections

General information:

- [Ansible Collection overview](https://github.com/ansible-collections/overview)
- [Ansible User guide](https://docs.ansible.com/ansible/latest/user_guide/index.html)
- [Ansible Developer guide](https://docs.ansible.com/ansible/latest/dev_guide/index.html)
- [Ansible Collections Checklist](https://github.com/ansible-collections/overview/blob/master/collection_requirements.rst)
- [Ansible Community code of conduct](https://docs.ansible.com/ansible/latest/community/code_of_conduct.html)

## Licensing

MIT
