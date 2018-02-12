# Introduction
Ansible playbooks and roles to automate the installation and configuration of the jenkins continuous integration server.

# Requirements

1. The solution runs on a clean installation of the chosen operating system without errors.
2. Jenkins and its prerequisites are installed without manual intervention.
3. Jenkins is configured to serve requests over port 8000 by default, but this can be overridden

# Testing

1. Tested using Ansible 2.2 and dynamic inventory for vagrant machines
2. Tested against a CentOS vagrant machine.
3. Tested with the Ansible controller being a Mac OS host system
3. Tested with Vagrant 2.x

# Assumptions

1. jenkins is installed without any plugins
2. jenkins is configured with 1 user (admin)
3. jenkins initial setup wizard (requiring manual intervention) should not be used; instead we should automate the preparation of the user and jenkins system

# Instructions

```
vagrant up default
ansible-playbook jenkins.yml
```

# Challenges

Jenkins 2.x now includes a security model and asks for Admin password upon initial start. This was a bit tricky to find a good solution to avoid this and use automation to properly setup Jenkins. Many solutions were found online but ultimately I found a very nice solution using Java options and a groovy initialisation script to create the first user.

# Idempotency

Pertains to subsequent applications of the solution not causing failures or repeating redundant configuration tasks. This is important in automation because it is a core philosophy of automation - it is generally referred to as “idempotency”. It means basically, the state of the target machine will remain as expected regardless of how many times you run a deployment or any automation scripts. For example, here we are checking the state of the Jenkins server to see if it is “started”. 

