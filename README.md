Ansible role for setting up rootless podman

## Supported Platforms

* Rocky Linux 8

## Requirements

Ansible 2.14+

```
ansible-galaxy install -r requirements.yml
```

## Example Playbook

Make sure the required collections are installed (see above under Requirements)

```yaml
---
- name: Example playbook
  hosts: podman_hosts
  become: true
  gather_facts: true

  vars:
    container_storage: /opt/containers/storage
    podman_user: podman
    podman_group: podman
    podman_runtime: crun

  roles:
    - role: ../ansible-role-podman
```
