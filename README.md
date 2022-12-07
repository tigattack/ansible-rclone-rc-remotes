# Ansible Role: rclone_rc_remotes

An Ansible role that creates Rclone remotes via Rclone's [rc API](https://rclone.org/rc).

Install the role: `ansible-galaxy install tigattack.rclone_rc_remotes`

## Requirements

None.

## Dependencies

None.

## Role Variables

- `rclone_host`: Rclone rc hostname or IP address. Defaults to `{{ ansible_fqdn }}`.
- `rclone_port`: Rclone rc port. Defaults to `5572`, rc's default port.
- `rclone_username`: Rclone rc username.
- `rclone_password`: Rclone rc password.
- `rclone_remotes`: List (array) of Rclone remotes.

`rclone_remotes` example, based on a simple Google Drive remote configuration:

```yml
rclone_remotes:
  - name: my-remote
    type: drive
    parameters:
      scope: drive
      client_id: "01234"
      client_secret: "56789"
      root_folder_id: "abcde"
```

## Rclone Remote Authentication

Some backend (remote) types, such as those which require OAuth, require interactive authentication and as such cannot be entirely automated.

In such cases, Ansible will prompt you with some instructions, pause execution, and ensure the remote can be connected once interactive authentication has been completed and you have resumed execution.

## Example Playbook

```yml
- hosts: all
  roles:
    - role: tigattack.rclone_rc_remotes
      vars:
        rclone_remotes:
          - name: my-remote
              type: drive
              parameters:
              scope: drive
              client_id: "01234"
              client_secret: "56789"
              root_folder_id: "abcde"
```

## Note on testing

This role is not tested automatically as it would require defining a usable remote for Rclone.

Please feel free to suggest a way this could be done without relying on a real-world service if you have any ideas.
