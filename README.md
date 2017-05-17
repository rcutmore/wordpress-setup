**Overview**

This is an Ansible playbook for setting up WordPress (using Apache and MariaDB) on a CentOS server.

**Getting Started**

Update Ansible hosts file (*/etc/ansible/hosts*) with production IP address:

    [production]
    Enter production server IP address here

Clone this repo to your local machine:

    git clone https://github.com/rcutmore/wordpress-setup.git
    cd ./wordpress-setup/

To set up development server:

    ansible-playbook ./development.yml

To set up production server:

    ansible-playbook ./production.yml

