# Goal

The Goal of this project is to demonstrate how to create a jenkins - docker pipeline which is fully automatically setup and can be used for any project.

When it should be possible to do the complete setup using the following steps:

Prerequisites:

1. Install Vagrant
2. Install the disksize plugin for vagrant by running:
```shell
vagrant plugin install vagrant-disksize
```

Finally setup a VM containing the Jenkins-Docker-Pipeline by running:
```shell
git clone git@github.com:ledergec/docker-jenkins-pipeline.git
git submodule update --init --recursive
vagrant up
```

You can then login to your new vm using:
```shell
vagrant ssh -- -X
```

Finally you can see jenkins in your browser by accessing http://localhost:8080

# Motivation

TODO

# Concept

1. Vagrant is used to setup a VM for example purposes
2. Within Vagrant ansible is used to setup jenkins including the complete configuration necessary
3. Then another project can be compiled / integrated by adding minimal configuration to jenkins. Jenkins will then simply build and run the dockercontainer including all the tests.
