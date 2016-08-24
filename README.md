# sshautomate

This repository contains:
  - Ansible playbook to automate the process of granting revoking SSH access to a server/group of servers for a new user.
  - A vagrant file which will create a virtual instance for demo/test

To use the vagrant file, you will need to have on your host,
 1. Vagrant
 2. VirtualBox
 3. Ansible

STEPS:

1. clone the repo - https://github.com/jithjose/sshautomate.git

2. cd to the directory contains Vagrantfile.
   run command: vagrant up

This creates 2 centos virtual instances (Instance1 :192.168.33.33 and Instance2:192.168.33.34 ) with VirtualBox, 
and runs the playbook which creates user "developer"in the instances and copy a SSH public key generated for user "developer"


To test:

   ssh -i developer-id_rsa developer@192.168.33.33  
   ssh -i developer-id_rsa developer@192.168.33.34

 It should log you on without a password ( hit yes for any initial SSH key addition warnings )


 To Revoke SSH access:-

 1a. Run the ansible playbook again with "action" provided as extra_vars.

   ansible-playbook --private-key=/<PATH_TO_HOMEDIR>/.vagrant.d/insecure_private_key  playbook.yml --extra-vars "action=absent"
   ( substitute  <PATH_TO_HOMEDIR> with appropriate path )

   OR

 1b.  Edit the playbook.yml and comment-out/comment-back the appropriate action within vars:

  vars:
  # action: present
    action: absent

    run playbook again -
    ansible-playbook --private-key=/<PATH_TO_HOMEDIR>/.vagrant.d/insecure_private_key  playbook.yml

