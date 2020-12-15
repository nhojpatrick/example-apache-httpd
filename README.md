# Apache Web Server Tutorial

Covers creating a basic apache httpd for learning and training.

Uses Vagrant to create and configure Virtual Box VM's, then Ansible to configure those VM's.

## 1. Overview

### Hosts
  1. Touchdown
  Used to configure webhost[0-2]. Uses ubuntu as centos has issues with shared file systems.

  1. webhost0
  Main web server we focus on, looking at virtual hosts and configuring a proxy for webhost1 and webhost2. Uses CentOS as it's most like RedHat

  1. webhost1
  Example backend server so webhost0 can demonstrate vhosts and proxies. Uses CentOS as it's most like RedHat

  1. webhost2
  Example backend server so webhost0 can demonstrate vhosts and proxies. Uses CentOS as it's most like RedHat

## 2. Setup Your ssh keys
```
$ ssh-keygen -f `pwd`/provisioning/.ssh/id_rsa
```

NOTE: Press enter to skip have a password for the ssh key

## 3. Create Env

All the webhost[0-2] are configured to auto boot, so a simple `vagrant up` will boot everything.

```
$ vagrant up
```

## 4. Create Touchdown

The touchdown server is not configured to auto boot, so needs to be explictly started.

```
$ vagrant up touchdown
```

## 5. Configure Apache

```
$ vagrant ssh touchdown
vagrant@touchdown:~$ cd /vagrant/setup/
vagrant@touchdown:/vagrant/setup$ ansible-galaxy collection install ansible.posix
vagrant@touchdown:/vagrant/setup$ ansible-galaxy install -r web_requirements.yaml
vagrant@touchdown:/vagrant/setup$ ansible-playbook -i hosts playbook.yaml
vagrant@touchdown:/vagrant/setup$
```
