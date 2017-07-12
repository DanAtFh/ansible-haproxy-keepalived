ansible-haproxy-keepalived
==========================

A playbook building high availability Load Balancer with HAProxy and keepalived. Comes preconfigured to be a frontend for this [MariaDB Galera Cluster] (https://bitbucket.org/fhcode/ansible-mariadb-galera-cluster).  

## Requirements

- [VirtualBox](https://www.virtualbox.org/wiki/Downloads). Tested on 5.1.x
- [Vagrant](http://www.vagrantup.com/downloads.html). Tested on 1.9.1
- [Ansible](http://docs.ansible.com/intro_installation.html). Tested on 2.3.1.0 

## Overview

It will install high availability Load Balancer with HAProxy and keepalived ready to deploy as a front end for the [MariaDB Galera Cluster].
You can customize it by editing vars file (var/main.yml).
Tested on Ubuntu 14.04 Trusty and CentOS 6.5.

## TODO / Wishlist

- upgrade Ubuntu to 16.04
- upgrade haproxy to the latest. 1.7.8 as of this writing.
- maybe merge these plays and vagrant file into the MariaDB Galera Cluster repo mentioned above.
- set up maintenance scripts for both front end and backend, e.g. use ansible to put backend servers into maintenance mode, apply updates and enable them again.

## Usage

- Edit vars/main.yml

- Test on Vagrant virtual machine(Requires Ansible).

```bash
$ vagrant up
```

- Install to remote server.

Edit `ansible_hosts`.

```
default ansible_ssh_host=xxx.xxx.xxx.xxx ansible_ssh_port=22
```

Run playbook.

```bash
ansible-playbook site.yml -i ansible_hosts
```

## vars

```vars/main.yml
haproxy_user: haproxy
haproxy_major_version: 1.5
haproxy_minor_version: 8
haproxy_download_url: "http://www.haproxy.org/download/{{ haproxy_major_version }}/src/haproxy-{{ haproxy_major_version }}.{{ haproxy_minor_version }}.tar.gz"
haproxy_src_dir: /tmp
haproxy_make_option: TARGET=linux2628 CPU=x86_64 USE_OPENSSL=1 USE_ZLIB=1 USE_PCRE=1
```

## Contributing

1. Fork it
2. Create your feature branch (`git checkout -b my-new-feature`)
3. Commit your changes (`git commit -am 'Add some feature'`)
4. Push to the branch (`git push origin my-new-feature`)
5. Create new Pull Request
