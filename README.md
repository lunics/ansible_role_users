# Ansible role: USERS

Setup groups, users accounts and users directories.

Can manage clear user password = always changed, or hash password = success if not changed and more secure.

Only tested on Archlinux.

## Usage
Override [defaults](https://github.com/lunics/ansible_role_users/blob/master/defaults/main.yml)
```yaml
user:
  - name:   foo             # required
    uid:    1000            # required
    group:  wheel           # optional, default = user.name (=foo)
    groups:                 # optional
      - video
      - kvm
      - libvirt
    passwd: "{{ vault.user.foo.hash }}"
    shell:  zsh             # optional, default = bash
    system: false           # optional, default = false
    create_home:            # optional, default = true
    state:  present         # optional, default = present
```
```yaml
group: []
  - name:   bar             # required
    gid:    4000            # required
    state:  present         # optional, default = present
    system: false           # optional, default = false
```
```yaml
user_dirs:                  # optional
  - owner: foo
    list:
      - downloads
      - .config
      - .config/systemd/user
      - .cache
      - .cache/logs
      - .cache/ansible
```
TODO
- user dirs not tested again
- replace user_dirs.list by user_dirs.path
