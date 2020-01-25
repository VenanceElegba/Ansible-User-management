# Users_Management_Ansible

# Install docker on ubuntu 
follow this link to install 

https://docs.docker.com/v17.12/install/linux/docker-ce/ubuntu/#set-up-the-repository

# Create Ansible User

adduser ansible

# Genarate SSH Key

https://www.digitalocean.com/community/tutorials/how-to-set-up-ssh-keys-on-ubuntu-1804

ssh-keygen

# Copy SSH Key to remote Users

ssh-copy-id username@remote_host

# Allow passwordless sudo 

visudo 

Add the following line to file 

        #includedir /etc/sudoers.d
		ansible      ALL=(ALL)       NOPASSWD: ALL

# Commande to execute ansible-playbook
Exemple: Create news users on the all host.

docker run --rm -it -v ~/.ssh/id_rsa:/root/.ssh/id_rsa -v ~/.ssh/id_rsa.pub:/root/.ssh/id_rsa.pub -v $(pwd):/ansible/playbooks philm/ansible_playbook  create-users.yml

# Execute playbook in specifique host

Exemple1: docker run --rm -it -v ~/.ssh/id_rsa:/root/.ssh/id_rsa -v ~/.ssh/id_rsa.pub:/root/.ssh/id_rsa.pub -v $(pwd):/ansible/playbooks philm/ansible_playbook  --limit host1 create-users.yml

Exemple2: docker run --rm -it -v ~/.ssh/id_rsa:/root/.ssh/id_rsa -v ~/.ssh/id_rsa.pub:/root/.ssh/id_rsa.pub -v $(pwd):/ansible/playbooks philm/ansible_playbook  --limit host1 host2 delete-users.yml

# Usefull link 

https://github.com/philm/ansible_playbook

NB: By default all playbook in this projet are set to run on all remote host specifiy in inventory file.
    Don't forget to execute Force_change_password.yml playbook to make users change password at first login.
    Add task for all news users you create to force password change for them by editing Force_change_password.yml.




