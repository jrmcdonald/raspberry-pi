# Rapsberry Pi Server Setup

## Overview

A set of Ansible scripts to manage a local Raspberry Pi server.

## Requirements

* [Ansible](https://www.ansible.com/)
* [GnuPG](https://gnupg.org/)

## Manual execution

*Note:* you must be keyed to the `.vault-pass` file to execute the playbooks.

From the project root:

```shell script
# configure virtualenv
virtualenv venv
source venv/bin/activate

# install python libraries
python -m pip install --upgrade pip
pip install -r requirements.txt

# install mitogen
ANSIBLE_STRATEGY=linear ansible-playbook mitogen.yaml

# install galaxy dependencies
ansible-galaxy install -r requirements.yaml

# bootstrap nodes & configure pi server
ansible-playbook -i production pi.yaml --become
```

To set up local config for an existing server:

```shell script
ansible-playbook -i production pi.yaml --become --tags "local" --skip-tags "pi"
```