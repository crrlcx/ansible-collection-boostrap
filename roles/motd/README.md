# About

Ansible role `motd` to manage MOTD and issue banners refreshed hourly by cron.
Uses fastfetch by default, neofetch on Debian Bookworm.

## Requirements

- Debian-based OS
- cron or systemd-cron

## Role variables

### Defaults

```yaml
bootstrap_motd: false              # enable/disable role in playbook

motd_cron_dir: /etc/cron.hourly    # directory for cron.hourly script
motd_cron_script: /etc/cron.hourly/motd # path to cron.hourly script
motd_dir: /etc/motd.d              # directory for motd files
motd_issue_dir: /etc/issue.d       # directory for issue files
```

### OS-specific variables (vars/)

Loaded automatically based on distribution release.
Output filenames are derived from `motd_bin` (`<motd_dir>/<motd_bin>`, `<motd_issue_dir>/<motd_bin>.issue`).

```yaml
# vars/debian/default.yml
motd_packages:
  - fastfetch
motd_bin: fastfetch

# vars/debian/bookworm.yml
motd_packages:
  - neofetch
motd_bin: neofetch
```

## Dependencies

- cron or systemd-cron

## Example playbook

```yaml
- hosts: servers
  collections:
    - crrlcx.bootstrap
  roles:
    - role: crrlcx.bootstrap.motd
```

## License

MIT
