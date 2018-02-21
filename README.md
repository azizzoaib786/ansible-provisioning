# Automated Setup of Virtual Machines

This repository contains a set of [Ansible][ansible] playbooks which are used to setup our [AWS EC2 machines][wiki-aws] in an automated way.

Although this is not an official part of the Fastlane product you can feel free to re-use this by creating a hard-fork and change it to your needs.

## Requirements:

* The machine running ansible needs to have SSH access
* The `centos` user on all hosts can use `sudo` without password

## Usage:

### Setup Ansible:

Ansible is a agent-less tool. Means you only need to install it on one host like your Workstation and/or your CI/CD Server. It performs all remote actions via plain SSH like for example Capistrano does.

```shell
$ brew install ansible       # On MacOS

$ apt-get install -y ansible # On Debian/Ubuntu

$ yum install -y ansible     # On RHEL/Centos
```

### Execute the Provisioning:

All changes can be applied with the following command:

```shell
$ ansible-playbook -i hosts site.yml
```

### Execute one Command on multiple Hosts:

Ansible can execute so called ad-hock commands on multiple hosts in paralell.

Example: Execute `docker ps` on all hosts in the **docker** group:

```shell
$ ansible -i hosts docker -a 'docker ps'
```

[ansible]: https://github.com/ansible/ansible
[wiki-aws]: https://github.fidor.de/fastlane/_internal/wiki/AWS
