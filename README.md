# Automated Setup of Virtual Machines

This repository contains a set of [Ansible][ansible] playbooks which are used to setup our [AWS EC2 machines][wiki-aws] in an automated way.

Although this is not an official part of the Fastlane product you can feel free to re-use this by creating a hard-fork and change it to your needs.

## Requirements:

* The machine running ansible needs to have SSH access
* The `centos` user on all hosts can use `sudo` without password

## Development:

The playbook can be tested with a local Vagrant machine:

```shell
$ vagrant up
$ vagrant provision
```

> **Note**:
>
> Currently not all roles are supported yet since they hardcode the `centos` username which does not exist in Vagrant.

## Usage:

### Setup Ansible:

Ansible is a agent-less tool. Means you only need to install it on one host like your Workstation and/or your CI/CD Server. It performs all remote actions via plain SSH like for example Capistrano does.

```shell
$ brew install ansible       # On MacOS

$ apt-get install -y ansible # On Debian/Ubuntu

$ yum install -y ansible     # On RHEL/Centos
```

### Execute the Provisioning:

#### On the static inventory (`hosts` file in this repo)

All changes can be applied with the following command:

```shell
$ ansible-playbook -i hosts --user centos site.yml
```

#### On a dynamic set of hosts:

```
$ HOSTS=docker01.example.com GROUPS=docker,docker-swarm-master ansible-playbook --user=centos --inventory=bin/hosts_from_env site.yml
```

### Execute one Command on multiple Hosts:

Ansible can execute so called ad-hock commands on multiple hosts in paralell.

Example: Execute `docker ps` on all hosts in the **docker** group:

```shell
$ ansible -i hosts docker --user centos -a 'docker ps'
```

### SSH config

Setup your ssh config to automatically use the `centos` user.

```
# ~/.ssh/config

Host *fastlane*.fidor.cloud
  User centos
  # IdentityFile ~/.ssh/id_rsa_xxxx.prv # optional
```

[ansible]: https://github.com/ansible/ansible
[wiki-aws]: https://github.fidor.de/fastlane/_internal/wiki/AWS
