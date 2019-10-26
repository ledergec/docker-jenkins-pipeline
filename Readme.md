# Goal

The Goal of this project is to demonstrate how to create a jenkins -
docker pipeline which is fully automatically setup and can be used for
any project.


When it should be possible to do the complete setup using the following steps:

Prerequisites:

1. Install Virtualbox
2. Install ansible
3. Install Vagrant
4. Install the disksize plugin for vagrant by running:
```shell
vagrant plugin install vagrant-disksize
```

Finally setup a VM containing the Jenkins-Docker-Pipeline by running:
```shell
git clone git@github.com:ledergec/docker-jenkins-pipeline.git
git submodule update --init --recursive
vagrant up
```

The VM will be reachable with the IP 192.168.50.4.

If can login to your new vagrant machine and do X-Forwarding by simply:
```shell
vagrant ssh -- -X
```

All relevant ssh information you need to connect to your machine can
retrieved by using:


Finally you can see jenkins in your browser by accessing http://localhost:8080

# Debugging Ansible Commands and Modules

In order to be able to run ansible without going through vagrant,
append your public key located in ~/.ssh/id_rsa.pub to the
~/.ssh/authorized_keys file within the vagrant machine. Use vagrant
ssh for doing this.

After adding this key you should be able to run an ansible from
command line as follows:
```shell
ansible-playbook playbook.yml -i hosts.yml -u vagrant
```

For debugging it may help to run ansible with the additional -vvvv
flag. Among other output you can find lines starting with "Using
module file" such as:
```shell
Using module file /usr/local/Cellar/ansible/2.7.10/libexec/lib/python3.7/site-packages/ansible/modules/web_infrastructure/jenkins_plugin.py
```

This information then allows you to find the location of the python
script associated with a given module. This can be edited in order to
obtain additional debug information. Make sure to make a backup before
doing so though!

Are there better ways to do this?!

# Installing a Jenkins Plugin

In order to add a jenkins plugin to the script you need to discover
its exact name and version. All existing plugins and versions are found at their
download site: http://mirrors.jenkins-ci.org/plugins/

Furthermore, sometimes the website address hosting the documentation of the
plugin may give a clear hint:

https://plugins.jenkins.io/workflow-durable-task-step

# Crutial Jenkins Plugins:

The configuration as code plugin allows configuring jenkins in a .yml file:
https://github.com/jenkinsci/configuration-as-code-plugin/blob/master/README.md
Here a folder with many demos of how to use the plugin can be found:
https://github.com/jenkinsci/configuration-as-code-plugin/tree/master/demos

The multibranch pipeline plugin:
https://plugins.jenkins.io/workflow-multibranch
https://jenkins.io/doc/book/pipeline/multibranch/

# Motivation

TODO

# Concept

1. Vagrant is used to setup a VM for example purposes
2. Within Vagrant ansible is used to setup jenkins including the
    complete configuration necessary.
3. Then another project can be compiled / integrated by adding minimal
   configuration to jenkins. Jenkins will then simply build and run
   the dockercontainer including all the tests.
   
