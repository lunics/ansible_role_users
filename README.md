# Ansible role: USERS

Setup groups, users accounts and users directories.

Can manage clear user password = always changed, or hash password = success if not changed and more secure.

Only tested on Archlinux.

## Usage
Create a directory in your host_vars/<hostname>/users/*.yml.
Or change the path of users_inventory_path.
Where each file in users_inventory_path is a user profile, see example below.

Override [defaults](https://github.com/lunics/ansible_role_users/blob/master/defaults/main.yml).

```yaml
# in file foo.yml
user:
  - name:   foo
    uid:    1002
    group:  wheel
    passwd: "{{ vault.user.foo.hash }}"
    shell:  zsh

# in file bar.yml
user:
  - name:   bar             # required
    uid:    1000            # required
    group:  wheel           # optional, default = user.name (=foo)
    groups:                 # optional
      - video
    passwd: "{{ vault.user.foo.hash }}"
    shell:  zsh             # optional, default = /bin/false
    system: false           # optional, default = false
    create_home: true       # optional, default = true
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
