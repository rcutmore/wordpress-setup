**Overview**

This is an Ansible playbook for setting up WordPress (using Apache and MariaDB) on a CentOS server.

**Getting Started**

Install Ansible:

    sudo yum install epel-release
    sudo yum install ansible

Update Ansible hosts file (*/etc/ansible/hosts*) with production IP address:

    [production]
    Enter production server IP address here

Clone this repo to your local machine:

    git clone https://github.com/rcutmore/wordpress-setup.git
    cd ./wordpress-setup/

Update variables (replace *[...]*'s):

    vi ./group_vars/all
    :%s/enter_db_name/[Enter WordPress database name]/g
    :%s/enter_db_username/[Enter WordPress database user]/g
    :%s/enter_db_password/[Enter WordPress database user password]/g
    :%s/enter_db_table_prefix/[Enter WordPress database table prefix]/g
    :%s/enter_os_user/[Enter OS user for managing WordPress]/g
    :x
    vi ./roles/mariadb/vars/main.yml
    :%s/enter_db_root_password/[Enter MariaDB root password here]/g
    :x
    vi ./roles/ssh/vars/main.yml
    :%s/enter_ssh_port/[Enter SSH port]/g
    :x
    vi ./roles/wordpress/vars/main.yml
    :%s/enter_website_domain/[Enter website domain]/g
    :x

To set up development server:

    ansible-playbook --ask-become-pass ./development.yml

To set up production server:

    ansible-playbook --ask-become-pass ./production.yml

