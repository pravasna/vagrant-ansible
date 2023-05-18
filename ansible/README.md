# Ansible Playbooks and Roles

## using public key to managed nodes

    ansible-playbook e45-ssh-addkey.yml -k
    password: vagrant
    ansible-playbook e45-ssh-addkey.yml - to check

### Installation and setup of webserver

    ansible-playbook e45-ntp-install.yml
    ansible-playbook e45-ntp-remove.yml
    ansible-playbook e45-ntp-template.yml
    ansible-playbook e46-site.yml

### Roles

    ansible-playbook e46-role-common.yml
    ansible-playbook e46-role-lb.yml
    ansible-playbook e46-role-web.yml
    ansible-playbook e46-role-site.yml

### Deployment strategies

    ansible-playbook e47-parallel.yml
    ansible-playbook e47-rolling.yml
    ansible-playbook e47-serial.yml

### Services Endpoint

#### <http://lb-ip/>

#### <http://web1/>

#### <http://web2/>
