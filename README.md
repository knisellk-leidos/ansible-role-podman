Ansible role for setting up rootless podman

## Supported Platforms

* Rocky Linux 8

## Requirements

Ansible 2.7 or higher is required for defaults/main/*.yml to work correctly.

## Variables

Variables for this role:

| variable | defaults/main/*.yml | type | description |
| -------- | ------------------- | ---- | ----------- |
| podman_enabled | False | boolean | determine whether role is enabled (true) or not (false) |
| podman_configure | False | boolean | use default configuration when False, write config, when True |
| podman_users | { root: '100000:65535' } | dictionary | podman users that get uid mapping configured |
| podman_manual_mapping | True | boolean | ansible managed /etc/subuid and /etc/subgid entries |
| podman_search_registries | - 'docker.io' | items | list of registries that podman is pulling images from |
| podman_insecure_registries | [] | items | non TLS registries for podman, i.e. localhost:5000 |
| podman_blocked_registries | [] | items | blocked container registries |
| podman_conf_cgroup_manager | 'systemd' | string | /etc/container/libpod.conf: cgroup_manager |
| podman_conf_events_logger | 'file' | string | /etc/container/libpod.conf: events_logger, due to podman error with journald, see [issue](https://github.com/containers/libpod/issues/3126) |
| podman_conf_namespace | '' | string | /etc/container/libpod.conf: namespace (=default namespace) |
| podman_storage_driver | 'overlay' | string | storage driver |
| podman_storage_mountopt | 'nodev' | string | storage driver mount options |

## Example Playbook

For a basic setup with default values run:

```yaml
---
# play: example-site
# file: site.yml

- hosts: podman_hosts
  vars:
    podman_enabled: True
    podman_users:
      root: '100000:65535'
      myuser1: '165536:65535'
      ...
    podman_registries:
      - 'registry.access.redhat.com'
      - 'docker.io'
      - 'registry.fedoraproject.org'
      - 'quay.io'
      - 'registry.centos.org'
  roles:
    - role: ansible-role-podman
```
