# Ansible Nexus OSS Role

[![Build Status](https://travis-ci.org/maaaikoool/ansible-nexus-oss.svg?branch=master)](https://travis-ci.org/maaaikoool/ansible-nexus-oss)

## Description

*ansible-nexus-oss* is an [Ansible](http://ansible.com) role.
Use this role to install Sonatype Nexus OSS.

## Provides

1. Latest Nexus OSS server

## Requires

1. Ansible 1.7 o higher
2. Ubuntu Server 14.04
3. Vagrant (optional)

## Usage

### Get the code

```bash
$ git clone git@github.com:codingbunch/ansible-nexus-oss.git
```

The code should reside in the roles directory of ansible ( See [ansible documentation](http://docs.ansible.com/playbooks.html#roles) for more information on roles ), in a folder named nexus.

### Create a host file

Following example make ansible aware of the Vagrant box reachable on localhost port 2222.

```bash
$ vi ansible.host
```

with

```ini
[nexus]
127.0.0.1 ansible_ssh_port=2222
```

### Create host specific variables

Make the host_vars directory where *ansible.host* file is located.

```bash
$ mkdir host_vars
```

Create a file in the newly created directory matching your host.

```bash
$ cd host_vars
$ vi 127.0.0.1
```

with

```yaml
---

timezone: Europe/Madrid

# NTP servers
ntp_server1: ntp0.ox.ac.uk
ntp_server2: ntp1.ox.ac.uk
ntp_server3: ntp2.ox.ac.uk
ntp_server4: ntp3.ox.ac.uk
ntp_server5: 0.uk.pool.ntp.org
ntp_server6: 1.uk.pool.ntp.org
ntp_server7: ntp.ubuntu.com # fallback

# NEXUS
nexus:
  version: 2.10.0
  unpackaged_version: 2.10.0-02
  base_dir: /opt
  home: /opt/nexus
  data_dir: /data
```

### Run the playbook

First create a playbook including the nexus role, naming it nexus.yml

```yml
- name: Nexus
  hosts: nexus
  roles:
    - nexus
```

Use *ansible.host* as inventory. Run the playbook only for the remote host *nexus*. Use *vagrant* as the SSH user to connect to the remote host. *-k* enables the SSH password prompt.

```bash
$ ansible-playbook -k -i ansible.host nexus.yml -u vagrant
```
