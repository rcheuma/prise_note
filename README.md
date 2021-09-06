

https://revolve.training/formations/architecting-on-aws-8/?gclid=EAIaIQobChMIlt6Nt73i8gIVVODtCh1D2wxZEAAYASAAEgKIGvD_BwE

http://training-class.akiros.it/terraform/


### TP-5 : [correction] code utilisé

NB: attention à l'indentation pour les fichiers yaml

cat hosts.yml
all:
vars:
ansible_ssh_common_args: '-o StrictHostKeyChecking=no'
prod:
hosts:
client:
ansible_host: 10.0.0.4

cat group_vars/prod.yml
ansible_user: admin
ansible_password: admin



cat deploy.yml

https://raw.githubusercontent.com/sadofrazer/ansible_training/master/webapp/webapp.yml
---

- name: "Apache installation using docker"

  hosts: Prod

  become: true

  vars:

  pre_tasks:

    - name: Install EPEL repo

      package: name=epel-release state=present

      when: ansible_distribution == "CentOS"



    - name: download pip script

      get_url:

        url: https://bootstrap.pypa.io/pip/2.7/get-pip.py

        dest: /tmp/get-pip.py



    - name: install python-pip

      command: python2.7 /tmp/get-pip.py



    - name: Install docker python

      pip: name=docker-py



  tasks:

    - name: Create Apache container

      docker_container:

        name: webapp

        image: httpd

        ports:

          - "80:80"



Install ansible lint

sudo yum install python-pip
sudo pip install ansible-lint
ansible-lint deploy.yml

ansible-playbook -i hosts.yml deploy.yml

Ansible verbose option
ansible-playbook -i hosts.yml -vvv deploy.yml

Push code
git init
git add .
git config --global user.email "diranetafen@yahoo.com"
git config --global user.name "dirane"
git commit -m "webapp first version"
git add origin
git push origin master