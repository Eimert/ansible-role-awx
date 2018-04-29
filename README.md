# Ansible Role: AWX (open source Ansible Tower)

[![Build Status](https://travis-ci.org/Eimert/ansible-role-awx.svg?branch=master)](https://travis-ci.org/Eimert/ansible-role-awx)

Installs and configures [AWX](https://github.com/ansible/awx), the open source version of [Ansible Tower](https://www.ansible.com/tower).

## Requirements

Before this role runs, assuming you want the role to completely set up AWX using it's included installer, you need to make sure the following AWX dependencies are installed:<br>
see [requirements.yml](requirements.yml).

## Role Variables

See [defaults/main.yml](defaults/main.yml).
```
# choose the inventory file to use. AWX default == inventory
inventory_file: inventory
```
Variable to control if awx will be installed immediately:
```
awx_run_install_playbook: yes
```
By default, this role will run the installation playbook included with AWX (which builds a set of containers and runs them). You can disable the playbook run by setting this variable to `no`.

Under [files/](files/) inventory files can be stored, that will be copied to the AWX host. Those files can be used to set custom PostgreSQL DB connection details. Like:
```
secret_key: awxsecret
pg_hostname: postgresql
pg_password: awxpass
pg_database: awx
pg_port: 5432
default_admin_user: admin
default_admin_password: password
```

## Dependencies

Depends on the roles defined in `requirements.yml`.

## Compatibility

- Red Hat Enterprise Linux 7
- CentOS 7
- Debian Jessie
- Debian Stretch
<br>
- Ansible >=2.3,<2.6

## Example Playbook and Inventory file

See playbook: [awx.yml](awx.yml). The [example-inventory](files/example-inventory) configures an external PostgreSQL db connection:
```
pg_hostname=ec2-79-125-112-209.eu-west-1.compute.amazonaws.com
pg_username=user123
pg_password=password321
pg_database=awx-dev-db
pg_port=5432
```

After AWX is installed, you can log in with the default username `admin` and password `password`.

## Troubleshooting

The default inventory files under files/ will enventually run out of sync with the [AWX project](https://github.com/ansible/awx/blob/devel/installer/inventory) inventory file. <br>
diff one inventory file with the latest default inventory file. Or rule out by using the AWX default inventory file downloaded at playbook run time:
```
# choose the inventory file to use. AWX default == inventory
inventory_file: inventory
```

## Development setup

Fork or `git clone git@github.com:Eimert/ansible-role-awx.git`.

    ansible-playbook -u eimertvink -i "ansible-dev.eimertvink.nl," ./awx.yml --start-at-task="Clone AWX into configured directory."


## License

MIT / BSD

## Author Information

This role was created in 2017 by [Jeff Geerling](https://www.jeffgeerling.com/), author of [Ansible for DevOps](https://www.ansiblefordevops.com/). <br>
2018: Eimert implemented customizable inventory/ files for more advanced installations, like an external PostgreSQL database connection.

