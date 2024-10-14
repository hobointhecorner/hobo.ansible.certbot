# hobo.ansible.certbot
Configure and run certbot via systemd timer with Ansible

## Requirements
Prerequisites:
- [Docker](https://github.com/hobointhecorner/Hobo.Ansible.Docker)

Ansible Collections:
- `community.general`

## Installation
[Ansible Galaxy](https://galaxy.ansible.com/docs/using/installing.html) can be used to install the role:

`ansible-galaxy install git+https://github.com/hobointhecorner/hobo.ansible.nginx.git[,<branch or commit hash>]`

## Variables
|                 Name                  |     Type     | Required |        Default         | Description |
|---------------------------------------|--------------|----------|------------------------|-------------|
| certbot_cert_domain                   | string       | **yes**  |                        | Domain for the requested certificate |
| certbot_cert_name                     | string       | **yes**  |                        | Name of the requested certificate |
| certbot_cert_email                    | string       | **yes**  |                        | Email to be associated with the requested certificate               |
| certbot_root_dir                   | string       | no       | /opt/hobo.certbot      | Directory where configuration files should be stored for all deployments.  Individual configurations will be stored in a subdirectory named the value of the `certbot_cert_name` variable |
| certbot_container_image               | string       | no       | certbot/certbot:latest | The certbot docker image to be run as a service |
| certbot_renewal_interval              | string       | no       | weekly                 | systemd `OnCalendar` value for the renewal timer |
| certbot_request_cert                  | bool         | no       | false                  | Perform initial certificate request |
| certbot_request_additional_parameters | string       | no       |                        | Additional command line parameters to pass to `certbot` |
| certbot_additional_volumes            | list(string) | no       |                        | Volumes to expose to the container. Uses `docker` cli syntax |
| certbot_user                          | string       | no       | certbot                | The user as which the service will be run.  Will have read/write access to the configuration directory |
| certbot_group                         | string       | no       | certbot                | The group the `certbot_user` user will be attached to.  Will have readonly access to the configuration directory |
| certbot_group_members                 | list(string) | no       |                        | Additional members to add to the `certbot_group` group |
