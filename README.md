# ROLE dginhoux.grub



## DESCRIPTION

This role configure grub bootloader.



## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip node with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `asserts_bypass=True`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.12

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.grub
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.grub dginhoux.grub
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.grub
      ansible.builtin.include_role:
        name: dginhoux.grub
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
grub_configure: "generate"

# the GRUB configuration variables
grub_config: {}

# grub user config file
grub_config_file: /etc/default/grub

# force GRUB to update its configuration
grub_force_update: false


# packages to be installed
grub_dependencies:
  - grub2

# extra GRUB dependencies to install (e.g. 'grub-btrfs')
grub_extra_dependencies: []

# GRUB dependencies to be removed
grub_remove_dependencies: "{{ ['os-prober'] if not ansible_os_family == 'RedHat' else [] }}"
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.

* Debian Family

```yaml
# grub mkconfig binary
grub_mkconfig_command: /usr/sbin/grub-mkconfig

# grub boot config file
grub_generated_config_file: /boot/grub/grub.cfg

# defaults for grub config
grub_config_defaults:
  # GRUB_DEFAULT: 0
  # GRUB_TIMEOUT: 10
  # GRUB_DISTRIBUTOR: "$(lsb_release -i -s 2> /dev/null || echo Debian)"
  # GRUB_CMDLINE_LINUX_DEFAULT: "quiet splash"
  # GRUB_HIDDEN_TIMEOUT: 0
  # GRUB_HIDDEN_TIMEOUT_QUIET: true
  # GRUB_CMDLINE_LINUX: ""
  # If you change this file, run 'update-grub' afterwards to update
  # /boot/grub/grub.cfg.
  # For full documentation of the options in this file, see:
  #   info -f grub -n 'Simple configuration'
  # GRUB_DEFAULT: 0
  GRUB_TIMEOUT: 5
  GRUB_DISTRIBUTOR: "$(lsb_release -i -s 2> /dev/null || echo Debian)"
  GRUB_CMDLINE_LINUX_DEFAULT: quiet
  # GRUB_CMDLINE_LINUX: ""
  # Disable os-prober, it might add menu entries for each guest
  GRUB_DISABLE_OS_PROBER: "true"
  # Uncomment to enable BadRAM filtering, modify to suit your needs
  # This works with Linux (no patch required) and with any kernel that obtains
  # the memory map information from GRUB (GNU Mach, kernel of FreeBSD ...)
  #GRUB_BADRAM: "0x01234567,0xfefefefe,0x89abcdef,0xefefefef"
  # Uncomment to disable graphical terminal (grub-pc only)
  #GRUB_TERMINAL: console
  # The resolution used on graphical terminal
  # note that you can use only modes which your graphic card supports via VBE
  # you can see them in real GRUB with the command `vbeinfo'
  #GRUB_GFXMODE: 640x480
  # Uncomment if you don't want GRUB to pass "root=UUID=xxx" parameter to Linux
  #GRUB_DISABLE_LINUX_UUID: "true"
  # Disable generation of recovery mode menu entries
  GRUB_DISABLE_RECOVERY: "true"
  # Uncomment to get a beep at grub start
  #GRUB_INIT_TUNE: "480 440 1"
```

* RedHat Family

```yaml
# grub mkconfig binary
grub_mkconfig_command: /usr/sbin/grub2-mkconfig

# grub boot config file
grub_generated_config_file: /boot/grub2/grub.cfg

# grub symlink config file_dest
grub_config_file_symlink: /etc/sysconfig/grub

# defaults for grub config
grub_config_defaults:
  # GRUB_DEFAULT: saved
  # GRUB_TIMEOUT: 1
  # GRUB_DISTRIBUTOR: "$(sed 's, release .*$,,g' /etc/system-release)"
  GRUB_CMDLINE_LINUX_DEFAULT: "crashkernel=auto quiet"
  # GRUB_DISABLE_RECOVERY: true
  # GRUB_DISABLE_SUBMENU: true
  # GRUB_TERMINAL_OUTPUT: console
  GRUB_TIMEOUT: 5
  GRUB_DISTRIBUTOR: "$(sed 's, release .*$,,g' /etc/system-release)"
  GRUB_DEFAULT: saved
  GRUB_DISABLE_SUBMENU: "true"
  GRUB_TERMINAL_OUTPUT: console
  # GRUB_CMDLINE_LINUX: "rhgb quiet selinux=0 crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M"
  # GRUB_CMDLINE_LINUX: "resume=/dev/mapper/vg0-lv--swap rd.lvm.lv=vg0/lv-root rd.lvm.lv=vg0/lv-swap rd.lvm.lv=vg0/lv-usr rhgb quiet selinux=0 crashkernel=1G-4G:192M,4G-64G:256M,64G-:512M"
  GRUB_DISABLE_RECOVERY: "true"
  GRUB_ENABLE_BLSCFG: "true"
```


## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
