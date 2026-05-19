# About

Ansible role `kmod` manages kernel module settings, initramfs module lists, modprobe options, and optional initramfs hooks.

## Requirements

- Linux target with Python
- `community.general` collection for `community.general.modprobe`
- `initramfs-tools` on Debian/Ubuntu-like systems if initramfs integration is needed

## Role variables

### Defaults

```yaml
bootstrap_kmod: false

# Provide initramfs hooks
kmod_initramfs_hooks_add: false

# Set RESUME=none
kmod_initramfs_resume_set: false
kmod_initramfs_resume: "none"

# List of kernel modules loaded at boot time
kmod_modules:
  - bfq
  - mq-deadline
  - kyber-iosched

# List of kernel modules included in initramfs
kmod_initramfs_modules:
  - lz4
  - lz4_compress
  - dm_cache
  - dm_cache_mq
  - dm_cache_smq
  - dm_persistent_data
  - dm_bufio
  - bfq
  - mq-deadline
  - kyber-iosched

# List of modprobe options: blacklist, install and options
kmod_modprobe_options:
  - "blacklist floppy"
  - "blacklist i2c_piix4"
  - "blacklist intel_powerclamp"
  - "options md_mod start_ro=1"
```

## Dependencies

None

## Example playbook

```yaml
- hosts: servers
  collections:
    - crrlcx.bootstrap
  roles:
    - role: crrlcx.bootstrap.kmod
```

## License

MIT
