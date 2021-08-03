# Ansible Role: Packer Linux Configuration for Vagrant

This role is intended for use with [Packer](http://www.packer.io/) to configure various linux distributions so they can then be used as a .box files for Vagrant deployment. It is specifically intended for use the following repo [boxes](https://github.com/jaredzieche/boxes.git). But you can use your own as well.

## Requirements

Before running this role via Packer, ansible needs to be installed using the shell provisioner. VM configuration (like adding a vagrant user to the appropriate group and the sudoers file) can be accomlplished with a Kickstart installation file (e.g. `kickstart.cfg`) using Packer. An example packer json file that wil call scripts and ansible roles based on your configuration:

    ```json
    "provisioners": [
      {
        "type": "shell",
        "execute_command": "echo 'vagrant' | {{.Vars}} sudo -S -E bash '{{.Path}}'",
        "script": "scripts/ansible.sh"
      },
      {
        "type": "ansible-local",
        "playbook_file": "../ansible/main.yml",
        "galaxy_file": "../ansible/requirements.yml"
      }
      ]
    ```

## Role Variables

{{ ansible_os_family }}{{ ansible_distribution_major_version }}_packages: This will allow the role to selectively install packages based on your chosen distribution.

## Dependencies

None.

## Example Playbook

    - hosts: all
      roles:
        - { role: jaredzieche.packerizer }

## License

MIT / BSD

## Author Information

This role was created in 2014 by [Jared Zieche](https://github.com/jaredzieche).