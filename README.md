slurm DevOps Upgrade Ansible practicum
=========

This is a final task as a prerequisit for certification

Description
------------

You can run playbook localy or inside VM.


Run inside VM 
--------------

vagrant --version
Vagrant 2.2.19

vagrant basebox https://app.vagrantup.com/bento/boxes/centos-7.9
more /etc/centos-release
CentOS Linux release 7.9.2009 (Core)

virtualbox --help
Oracle VM VirtualBox VM Selector v6.1.38

ansible --version
ansible 2.9.27
  config file = /etc/ansible/ansible.cfg
  configured module search path = [u'/home/vagrant/.ansible/plugins/modules', u'/usr/share/ansible/plugins/modules']
  ansible python module location = /usr/lib/python2.7/site-packages/ansible
  executable location = /usr/bin/ansible
  python version = 2.7.5 (default, Nov 16 2020, 22:23:17) [GCC 4.8.5 20150623 (Red Hat 4.8.5-44)]


Bring VM up:

vagrant up server_centos_ansible

During bringing up vm vagrant installs ansible, git and makes git clone 

SSH to VM:

vagrant ssh server_centos_ansible

Change path to cloned git repo:

cd slurm_ansible/

Just in case run:

ansible-galaxy install -r requirements.yml

The following variables (secrets) must be defined in file "group_vars/all/vault.yml" and encrypted with ansible-vault: 

slurm_git_user: XXXXXX
slurm_git_password: XXXXXX

ansible-vault encrypt group_vars/all/vault.yml

After secrets are added use the following command to run playbook:

ansible-playbook -i hosts --vault-password-file files/vault_password playbook.yml


"files/vault_password" must contain password that is used to encrypt "group_vars/all/vault.yml" 


Variables
--------------

If you need change the following variables

secret: mysecret
rails_env: production
db_host: 127.0.0.1
db_port: 5432
db_name: xpaste_db
db_user: xpaste_user
db_password: xpaste_password
working_dir: /opt/app

Variables are inherited and used in roles install_app, install_postgres and nginx 
You can redefine variables in install_app/vars and install_postgres/vars but it is a bad idea.

Dependencies
------------

-

Example Playbook
----------------

-