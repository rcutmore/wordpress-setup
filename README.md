**Overview**

This is an Ansible playbook for setting up WordPress (using Apache and MariaDB) on a CentOS server.

**Getting Started**

Update Ansible hosts file (*/etc/ansible/hosts*) with production IP address:

    [production]
    Enter production server IP address here

Clone this repo to your local machine:

    git clone https://github.com/rcutmore/wordpress-setup.git
    cd ./wordpress-setup/

Update variables (replace *[...]*'s):

    vi ./roles/mariadb/vars/main.yml
    :%s/enter_db_root_password/[Enter MariaDB root password here]/g
    :%s/enter_wordpress_db_name/[Enter WordPress database name here]/g
    :%s/enter_wordpress_db_user/[Enter database user here]/g
    :%s/enter_wordpress_db_user_password/[Enter database user password here]/g
    :x

To set up development server:

    ansible-playbook --ask-become-pass ./development.yml

To set up production server:

    ansible-playbook --ask-become-pass ./production.yml

