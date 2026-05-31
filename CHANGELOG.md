# Changelog

All notable changes to the `crrlcx.bootstrap` Ansible collection will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.8.6] - 2026-05-31

### Added

- `inadyn` role: added support for Ubuntu Jammy with version 2.8.1.

## [1.8.5] - 2026-05-19

### Fixed

- `kmod` role: removed `ansible_managed` comment from the 'copy' content to prevent undefined variable errors.

## [1.8.4] - 2026-05-19

### Changed

- `repositories` role: moved loop for Debian modern repositories to improve task structure.
- `kmod` role: enhanced tasks for improved functionality.

## [1.8.0] - 2026-05-19

### Added

- `kmod` role: manage kernel module settings, initramfs modules, and modprobe options.

### Changed

- `bootstrap` playbook: include `kmod` role with conditional execution.
- Documentation: added README and task files for `kmod`.

## [1.7.4] - 2026-05-09

### Changed

- `ssh` role: Updated role license to MIT, modified tasks for improved functionality.

## [1.7.3] - 2026-04-30

### Changed

- `repositories` role: add handler to strip carriage returns from `.asc` keyring files under `/etc/apt/keyrings` before updating apt cache.

## [1.7.2] - 2026-04-27

### Added

- `motd` role: added `motd_cron_dir` variable to configure the cron.hourly directory path.

### Changed

- `motd` role: changed `motd_cron_script` default from full path to filename (`motd`).
- `motd` role: cron script destination is now built from `{{ motd_cron_dir }}/{{ motd_cron_script }}`.
- `motd` role: ensure `motd_cron_dir` directory exists before deploying the script.

## [1.7.1] - 2026-03-20

### Added

- `inadyn` role for dynamic DNS client configuration.
- All roles: add `inadyn` role to the `playbook/bootstrap.yml` with feature flag.

### Changed

- **BREAKING:** `hosts` role: replaced `hosts_file_conditions` variable with `hosts_file` for direct file path specification.

### Fixed

- All roles: fixed FQCN issue at the `playbook/ping.yml` to `ansible.builtin.ping` for connectivity testing.

## [1.6.25] - 2026-03-08

### Changed

- **BREAKING:** Removed `become: true` from all tasks and handlers across all roles — must be set at play or role level now.
- **BREAKING:** `disk` role: removed AWS NVMe EBS support (`disk-aws-nvme-ebs.yml` and `disk_config.py` custom module deleted).
- **BREAKING:** `hosts` role: removed `is defined` checks for `hosts_hostname` / `hosts_hostname_fqdn` — variables must be defined (empty string is OK).
- All roles: migrated to FQCN (`ansible.builtin.*`, `ansible.posix.*`, `community.general.*`).
- All roles: standardized task names (removed role prefix, capitalized).
- `disk` role: replaced `with_items` with `loop`, added `changed_when`/`check_mode` where needed.
- `disk` role: OS-aware `scsitools`/`sg3_utils` package selection.
- `dns`, `ntp`, `udev` roles: added `flush_handlers` meta task.
- `dns`, `ntp` roles: fixed handler listen directives.
- `lvm` role: migrated to `community.general.lvol`, `community.general.lvg`, `community.general.filesystem`.
- `sysctl` role: migrated to `ansible.posix.sysctl`.
- File mode notation standardized to octal strings (`"0644"`) across all roles.

### Removed

- `disk` role: removed `library/disk_config.py` custom module.
- `disk` role: removed `tasks/disk-aws-nvme-ebs.yml`.
- `ssh` role: removed `become: true` from handler and include.

## [1.6.1] - 2026-03-01

### Changed

- `ca` role: added handler flush after certificate tasks for immediate trust store update.

### Removed

- `ca` role: removed RedHat CA update handler (Debian-only now).

## [1.6.0] - 2026-03-01

### Added

- `ca` role: support downloading certificates from URL via `get_url`.
- `ca` role: support installing certificates from inline content via `copy`.

### Changed

- **BREAKING:** `ca` role completely reworked — old variables removed, new `ca_certificates` list replaces `ca_src_fileglob` and `ca_path` dictionary.
- **BREAKING:** `ca` role no longer copies certificates from local fileglob (`with_fileglob`). Use `ca_certificates` with `url` or `content` instead.
- `ca` role: simplified destination path to single `ca_dest` variable (default: `/usr/local/share/ca-certificates`).
- `ca` role: handlers use FQCN and `changed_when: false`.
- `grub` role: minor handler fix.
- `ntp`, `udev` roles: added missing handler attributes.

### Removed

- `ca` role: removed `ca_src_fileglob`, `ca_path`, `ca_path_debian_default` variables.
- `ca` role: removed RHEL 6 `update-ca-trust enable` task.
- `ca` role: removed `files/ca.crt` placeholder.

## [1.5.5] - 2026-03-01

### Changed

- Refactored variable registrations across multiple roles for improved clarity.
- Enhanced `grub` role: updated handlers and task flow.
- Refactored `swap` role: improved handlers and task logic for swapfile management.
- Refactored `disk` role: updated AWS NVMe EBS task variable names.
- Refactored `repositories` role: cleaned up task variable registrations.

## [1.5.0] - 2026-03-01

### Added

- `grub` role for GRUB bootloader configuration management.

## [1.4.23] - 2026-02-28

### Added

- `python3-debian` package dependency in `repositories` role defaults.
- APT version gathering for conditional task logic in `repositories` role.

### Changed

- Enhanced `repositories` role task flow based on APT version detection.

## [1.4.20] - 2026-02-28

### Added

- OS-specific variables for `motd` role (`vars/debian/bookworm.yml`, `vars/debian/default.yml`).

### Changed

- Refactored `motd` role tasks for better OS compatibility.
- Updated `motd` README and streamlined variable definitions.
- Simplified `motd` template.

## [1.4.12] - 2026-02-28

### Changed

- Refactored `repositories` role: remove legacy repositories before adding new ones in DEB822 format.
- Standardized architecture to `amd64` in `debian-modern` task.

## [1.4.10] - 2026-02-27

### Changed

- Refactored `motd` role: updated README, streamlined variable definitions, fixed loop using `{{ item }}`.
- Removed non-existent `tee` package from `motd` defaults.
- Switched `motd` tasks to `ansible.builtin.package` module.

## [1.4.4] - 2026-02-27

### Changed

- Refactored `swap` role: streamlined README, updated defaults, reorganized task files.
- Updated README and removed unused environment variables in `dns`, `ntp`, `udev` task files.
- Updated `ca` role README.

### Removed

- Removed `systemd-swap` support and bundled deb package from `swap` role.

## [1.4.0] - 2026-02-27

### Added

- `repositories` role for APT repository management (legacy and DEB822 formats).
- This changelog file.

## [1.3.1] - 2022-11-16

### Changed

- Updated feature flags in bootstrap playbook.
- Miscellaneous improvements and fixes.

## [1.3.0] - 2022-10-13

### Added

- `hosts` role for hostname and `/etc/hosts` management.

## [1.2.55] - 2022-10-13

### Added

- `udev` role for udev rules management.

## [1.1.8] - 2022-10-12

### Added

- `dns` role for DNS resolver configuration.
- `ping.yml` playbook for connectivity testing.
- Feature flags in `bootstrap.yml` playbook (`bootstrap_hosts`, `bootstrap_sysctl`, etc.).

### Changed

- Renamed `timesyncd` role to `ntp`.
- Disabled IPv6 configuration by default.

## [1.0.7] - 2022-09-20

### Changed

- Documentation updates.
- CI linting improvements.
- Build ignore patterns for Galaxy packaging.

## [1.0.0] - 2022-09-20

### Added

- Initial release of the `crrlcx.bootstrap` collection.
- Roles: `bootstrap`, `ca`, `ntp`, `ssh`, `motd`, `sysctl`.
- Bootstrap playbook for orchestrating all roles.

[1.6.25]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.6.1...1.6.25
[1.6.1]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.6.0...1.6.1
[1.6.0]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.5.5...1.6.0
[1.5.5]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.5.0...1.5.5
[1.5.0]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.4.23...1.5.0
[1.4.23]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.4.20...1.4.23
[1.4.20]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.4.12...1.4.20
[1.4.12]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.4.10...1.4.12
[1.4.10]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.4.4...1.4.10
[1.4.4]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.4.0...1.4.4
[1.4.0]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.3.1...1.4.0
[1.3.1]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.3.0...1.3.1
[1.3.0]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.2.55...1.3.0
[1.2.55]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.1.8...1.2.55
[1.1.8]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.0.7...1.1.8
[1.0.7]: https://github.com/crrlcx/ansible-collection-bootstrap/compare/1.0.0...1.0.7
[1.0.0]: https://github.com/crrlcx/ansible-collection-bootstrap/releases/tag/1.0.0
