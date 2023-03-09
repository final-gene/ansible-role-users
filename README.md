# Ansible Role `users`

## Description

This role allows to manage users and user groups on a system.

## Requirements

The collection `ansible.posix` is required to use this role.
```shell
ansible-galaxy collection install ansible.posix
```

## Role Variables

| Variable                           | Type            | Default                | Comments                                                                                                                                            |
|------------------------------------|-----------------|------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------|
| users                              | list of objects | `[]`                   | List of users to create/delete (see [users](#users)).                                                                                               |
| users_authorized_keys_exclusive    | boolean         | `true`                 | Default user's setting for authorized keys exclusive.                                                                                               |
| users_authorized_keys_file         | string          | `.ssh/authorized_keys` | Path to the `authorized_keys` file inside the user's home directory.                                                                                |
| users_create_homedirs              | boolean         | `true`                 | Create home directories for new users.                                                                                                              |
| users_create_per_user_group        | boolean         | `true`                 | Create a group for every user and make that their primary group if set to `true`.                                                                   |
| users_default_shell                | string          | `/bin/bash`            | The default shell for a user if none is specified.                                                                                                  |
| users_group                        | string          | `users`                | The default group name all users belong to.<br>Only required if `users_create_per_user_group` is set to `false`.                                    |
| users_groups                       | list of objects | `[]`                   | List of user groups to create/delete (see [users_groups](#users_groups)).                                                                           |
| users_home                         | string          | `/home`                | The directory which will contain all user home directories.                                                                                         |
| users_home_chroot                  | boolean         | `false`                | The default user's home directory chroot setting.                                                                                                   |
| users_home_mode                    | string          | `0750`                 | The default user's home directory permissions.                                                                                                      |
| users_kill_process                 | boolean         | `false`                | Kill user process if user is in use.                                                                                                                |
| users_kill_process_allowed_users   | list of strings |                        | List of user names which processes should be killed.<br>Only used if `users_kill_processes` is set to `true`.                                       |
| users_kill_process_forbidden_users | list of strings | `[]`                   | List of user names which processes should never be killed.<br>`root` is always prohibited!<br>Only used if `users_kill_processes` is set to `true`. |
| users_kill_process_timeout         | integer         | `30`                   | Time to wait before force kill a process.<br>Only used if `users_kill_processes` is set to `true`.                                                  |
| users_ssh_key_type                 | string          | `rsa`                  | Default user's ssh key type.                                                                                                                        |

### users

| Variable                  | Type                 | Default   | Comments                                                                                                                                                             |
|---------------------------|----------------------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| append                    | boolean              | `false`   | Existing group relations will not be removed if set to `true`.                                                                                                       |
| authorized_keys           | list of strings      |           | List of public keys for ssh authorization.                                                                                                                           |
| authorized_keys_exclusive | list of strings      |           | Existing public keys for authorization will not be removed if set to `true`.                                                                                         |
| comment                   | string               | `''`      | Regular name of the user stored as comment.                                                                                                                          |
| expires                   | integer              |           | An expiry time for the user in epoch.                                                                                                                                |
| force                     | boolean              | `false`   | This only affects `state=absent`, it forces removal of the user and associated directories on supported platforms.                                                   |
| group                     | string               |           | The of the user's primary group.                                                                                                                                     |
| groups                    | list of strings      |           | A list of all groups the user belongs to.                                                                                                                            |
| home                      | string               |           | Absolute path to the user's home directory.                                                                                                                          |
| home_chroot               | boolean              |           | Set home ownership to `root` to allow chroot feature for user home directories.                                                                                      |
| home_create               | boolean              |           | Create the user's home directory.                                                                                                                                    |
| home_files                | list of objects      |           | List of files which should be managed within the users home directory.                                                                                               |
| home_mode                 | string               |           | The user's home directory permissions.                                                                                                                               |
| local                     | boolean              | `false`   | Forces the use of “local” command alternatives on platforms that implement it.                                                                                       |
| move_home                 | boolean              | `false`   | If set to `true` when used with `home:`, attempt to move the user’s old home directory to the specified directory if it isn’t there already and the old home exists. |
| non_unique                | boolean              | `false`   | Optionally when used with the -u option, this option allows to change the user ID to a non-unique value.                                                             |
| password                  | string               | `!`       | The user's password hash (should be created with `mkpasswd`).                                                                                                        |
| password_expire_max       | integer              |           | Maximum number of days between password change.                                                                                                                      |
| password_expire_min       | integer              |           | Minimum number of days between password change.                                                                                                                      |
| password_lock             | boolean              |           | Lock the password.                                                                                                                                                   |
| remove                    | boolean              | `false`   | This only affects `state=absent`, it attempts to remove directories associated with the user.                                                                        |
| seuser                    | string               |           | Optionally sets the seuser type (user_u) on selinux enabled systems..                                                                                                |
| shell                     | string               |           | The user's logon shell.                                                                                                                                              |
| ssh_key_bits              | integer              |           | Size of the generated ssh key.                                                                                                                                       |
| ssh_key_comment           | string               |           | Optionally define the comment for the SSH key.                                                                                                                       |
| ssh_key_file              | string               |           | Optionally specify the SSH key filename.                                                                                                                             |
| ssh_key_generate          | boolean              |           | Generate a ssh key pair if set to `true`.                                                                                                                            |
| ssh_key_password          | string               |           | Passphrase for the generated ssh key.                                                                                                                                |
| ssh_key_type              | string               |           | Type of the generated ssh key (`rsa`, `ed25519`, etc.).                                                                                                              |
| ssh_keys                  | list of objects      |           | List of private ssh keys to provide for the user (see [ssh_keys](#ssh_keys)).                                                                                        |
| state                     | string               | `present` | `present` will create or update the user.<br>`absent` will remove an existing user.                                                                                  |
| system                    | boolean              |           | Weather the user is a system user (`true`) or not (`false`).                                                                                                         |
| uid                       | integer              |           | The user's UID. If not defined, the create process will use the nex available UID.                                                                                   |
| update_password           | boolean              |           | `always` will update passwords if they differ.<br>`on_create` will only set the password for newly created users.                                                    |
| username                  | string<br>_required_ |           | Login name of the user.                                                                                                                                              |

### home_files

| Variable  | Type    | Default   | Comments                                                                            |
|-----------|---------|-----------|-------------------------------------------------------------------------------------|
| content   | string  |           | Content of the managed file (only used when `template` is not defined).             |
| dir_mode  | string  | `0750`    | Directory permissions (only used if directories have to be created).                |
| file_mode | string  | `0640`    | File permissions.                                                                   |
| path      | string  |           | File path, relative to the users home directory.                                    |
| state     | string  | `present` | `present` will create or update the file.<br>`absent` will remove an existing file. |
| template  | string  |           | Weather the group is a system group (`true`) or not (`false`).                      |

### ssh_keys

| Variable | Type                 | Default   | Comments                                                                                                      |
|----------|----------------------|-----------|---------------------------------------------------------------------------------------------------------------|
| name     | string<br>_required_ |           | Name of the key file.                                                                                         |
| key      | string               |           | SSH private key file content.                                                                                 |
| state    | string               | `present` | `present` will store the key file in the user's home directory.<br>`absent` will remove an existing key file. |

### users_groups

| Variable | Type                 | Default   | Comments                                                                              |
|----------|----------------------|-----------|---------------------------------------------------------------------------------------|
| gid      | integer              |           | The groups GID. If not defined, the create process will use the nex available GID.    |
| local    | boolean              | `false`   | Forces the use of “local” command alternatives on platforms that implement it.        |
| name     | string<br>_required_ |           | Name of the group.                                                                    |
| state    | string               | `present` | `present` will create or update the group.<br>`absent` will remove an existing group. |
| system   | boolean              |           | Weather the group is a system group (`true`) or not (`false`).                        |

## Example Playbook

```yaml
users:
  - username: foo
    comment: Foo Barrington
    groups:
      - wheel
      - -systemd-journal
    uid: 1001
    home: /local/home/foo
    authorized_keys:
      - "ssh-rsa AAAAA.... foo@machine"
      - "ssh-rsa AAAAB.... foo2@machine"
  - username: bar
    uid: 1002
    state: absent
    remove: yes
    force: yes
users_groups:
  - name: developers
    gid: 10000
```
