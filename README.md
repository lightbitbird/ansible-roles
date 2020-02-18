# ansible-roles
### Ansible role examples

#
### Installing

**Install virtualbox and vagrant**

https://www.virtualbox.org/

https://www.vagrantup.com/


**Install Ansible**

You need to install python, pip and virtualenv before installing Ansible.

```
# Install Ansible after python, pip virtualenv
$ python -m venv env
$ source env/bin/activate
(env)$ pip install ansible
```

#
### Vagrant setup and run
```
$ mkdir centos7
$ cd centos7
$ vagrant box add centos/7

# vagrant asks which provider you will choose, then select 3) virtualbox

# confirm the centos/7 installed
$ vagrant box list
$ vim Vagrantfile
# add the following texts.

  config.vm.define :node1 do |node|
    node.vm.box = "centos6"
    node.vm.network :forwarded_port, guest: 22, host: 2001, id: "ssh"
    node.vm.network :private_network, ip: "192.168.33.11"
  end

  config.vm.define :node2 do |node|
    node.vm.box = "centos6"
    node.vm.network :forwarded_port, guest: 22, host: 2002, id: "ssh"
    node.vm.network :forwarded_port, guest: 80, host: 8000, id: "http"
    node.vm.network :private_network, ip: "192.168.33.12"
  end

# boot the nodes.
$ vagrant up
# check ssh
$ vagrant ssh node1
$ vagrant ssh node2
```

#
### Ansible setup and run
```
$ cd ansible-roles
$ python -m venv env
$ source env/bin/activate
(env)$ pip install ansible
# check host node1's ping 
(env)$ ansible -i hosts 192.168.33.11 -m ping

# Install nginx and run with Ansible
(env)$ ansible-playbook -i hosts playbooks/list.yml
(env)$ ansible-playbook -i hosts playbooks/loadbalancer.yml
```

