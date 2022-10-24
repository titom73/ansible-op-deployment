# One Password CLI deployment

A simple ansible role to deploy [one-password cli](https://1password.com/fr/downloads/command-line/) manager on many platforms

It supports deployment for the following platform:

- `amd64`: For x86_64 bits processor
- `arm` for raspberry Pi3
- `arm64` for raspberry Pi4


## installation

```shell
ansible-galaxy collection install titom73.op_deployment
```

## Requirements

System must have following binaries:

- `wget`
- `unzip`

## Role Variables

Role comes with many different variables with default value:

```yaml
# Configure role to install or remove op binary
op_deployment_state: present

# Should we force binary update or ignore if binary is already installed
op_deployment_force_update: true

# Target platform (arm/arm64/amd64)
op_deployment_platform: amd64

# one-password cli version to install
op_deployment_version: 'v2.7.2'
```

Also, you can modify installation path:

```yaml
# Name of the binary to install
op_deployment_bin: 'op'

# Path where to install binary
op_deployment_installation_path: '/usr/local/sbin/'

# Full binary path
op_deployment_bin_path: '{{ op_deployment_installation_path }}/{{ op_deployment_bin }}'

# Path to temporary filesystem
op_deplyment_tmp: /tmp
```

## Dependencies

None

## Example Playbook

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yaml
- name: Install One Password CLI manager
  hosts: linux_machines
  gather_facts: true
  become: true
  tasks:

    - name: Install ONE Password CLI
      tags: [password]
      import_role:
        name: roles/one-password-deploy
      vars:
        op_deployment_platform: 'arm'
        op_deployment_version: 'v2.7.1'
```

## License

BSD

## Author Information

This role was created in 2022 by [Thomas Grimonet](https://github.com/titom73)