Ansible Role : dginhoux.grub
=========

This ansible role configure grub


Requirements
------------

This role require a supported platform defined in `meta/main.yml`.
It will skip node with unsupported platform ; this behaviour can be bypassed by settings this variable `asserts_bypass=True`.


Role Variables
--------------

Necessary variables are defined on `defaults/main.yml`.

```yaml
# main switch
grub_configure: "generate"

# the GRUB configuration variables
grub_config: {}

# grub user config file
grub_config_file: /etc/default/grub

# force GRUB to update its configuration
grub_force_update: false
```

Specifics variables are in `vars/{{ ansible_os_family }}` ; example for RedHat OS family : 

```yaml
# grub mkconfig binary
grub_mkconfig_command: /usr/sbin/grub2-mkconfig

# grub boot config file
grub_generated_config_file: /boot/grub2/grub.cfg

# grub symlink config file_dest
grub_config_file_symlink: /etc/sysconfig/grub

# defaults for grub config
grub_config_defaults:
  GRUB_CMDLINE_LINUX_DEFAULT: "crashkernel=auto quiet"
  GRUB_TIMEOUT: 5
  GRUB_DISTRIBUTOR: "$(sed 's, release .*$,,g' /etc/system-release)"
  GRUB_DEFAULT: saved
  GRUB_DISABLE_SUBMENU: "true"
  GRUB_TERMINAL_OUTPUT: console
  GRUB_DISABLE_RECOVERY: "true"
  GRUB_ENABLE_BLSCFG: "true"
```



Dependencies
------------

none


Example Playbook
----------------



License
-------

BSD ; This role is inspired from https://github.com/aisbergg/ansible-role-grub


Author Information
------------------

https://github.com/dginhoux/
