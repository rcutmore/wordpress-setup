**Overview**

This contains Ansible playbooks for setting up WordPress (using Apache
and MariaDB) on a CentOS server. Currently these playbooks are not
idempotent, they are meant to be run once to set up the server but
running them multiple times will result in errors.


**Prerequisites**

Install and start SSH server on WordPress server:

    sudo yum install openssh-server
    sudo systemctl start sshd

SSH server should be running with defaults. At the very least it must
be listening on port 22.

Upload SSH key from Ansible host to WordPress server:

    ssh-keygen -b 4096 -t rsa
    ssh-copy-id <Enter OS user on WordPress server>@<Enter WordPress server IP address>

**Getting Started**

Install Ansible:

    sudo yum install epel-release
    sudo yum install ansible

Update Ansible hosts file (*/etc/ansible/hosts*) with production IP address:

    [wordpress-server]
    <Enter server IP address here> ansible_connection=ssh ansible_ssh_user=<Enter SSH user here> ansible_ssh_pass=<Enter SSH password here>

Clone this repo to your local machine:

    sudo yum install git
    git clone https://github.com/rcutmore/wordpress-setup.git
    cd ./wordpress-setup/

Update variables (replace all *[...]*):

    vi ./group_vars/all
    :%s/enter_db_name/[Enter WordPress database name]/g
    :%s/enter_db_username/[Enter WordPress database user]/g
    :%s/enter_db_password/[Enter WordPress database user password]/g
    :%s/enter_db_table_prefix/[Enter WordPress database table prefix]/g
    :%s/enter_os_user/[Enter OS user for managing WordPress]/g
    :%s/enter_ssh_port/[Enter SSH port]/g
    :x
    vi ./roles/fail2ban/vars/main.yml
    :%s/enter_dest_email/[Enter destination email address]/g
    :x
    vi ./roles/mariadb/vars/main.yml
    :%s/enter_db_root_password/[Enter MariaDB root password here]/g
    :x
    vi ./roles/wordpress/vars/main.yml
    :%s/enter_website_domain/[Enter website domain]/g
    :x

To set up development server:

    ansible-playbook --ask-become-pass ./development.yml

To set up production server:

    ansible-playbook --ask-become-pass ./production.yml

