
https://docker.labs.eazytraining.fr/
https://revolve.training/formations/architecting-on-aws-8/?gclid=EAIaIQobChMIlt6Nt73i8gIVVODtCh1D2wxZEAAYASAAEgKIGvD_BwE

http://training-class.akiros.it/terraform/

https://www.youtube.com/watch?v=RSXmQMceyzs

https://kodelabs.gitlab.io/k3g/#0

https://excalidraw.com/

https://www.youtube.com/watch?v=URcMBXjIr24


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

##################################################################################
dockerfile
##################################################################################
FROM php:7.4-fpm

ENV PHP_SECURITY_CHECHER_VERSION=1.0.0

RUN apt-get update && apt-get install -y \
      wget \
      git \
      fish

RUN apt-get update && apt-get install -y libzip-dev libicu-dev && docker-php-ext-install pdo zip intl opcache

# Support de apcu
RUN pecl install apcu && docker-php-ext-enable apcu

# Support de redis
RUN pecl install redis && docker-php-ext-enable redis

# Support de Postgre
RUN apt-get update && apt-get install -y libpq-dev && docker-php-ext-install pdo_pgsql

# Support de MySQL (pour la migration)
RUN docker-php-ext-install mysqli pdo_mysql

# Imagick
RUN apt-get update && apt-get install -y libmagickwand-dev --no-install-recommends && pecl install imagick && docker-php-ext-enable imagick

# Composer
RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/bin/ --filename=composer

# Symfony tool
RUN wget https://get.symfony.com/cli/installer -O - | bash && \
  mv /root/.symfony/bin/symfony /usr/local/bin/symfony

# Security checker tool
RUN curl -L https://github.com/fabpot/local-php-security-checker/releases/download/v${PHP_SECURITY_CHECHER_VERSION}/local-php-security-checker_${PHP_SECURITY_CHECHER_VERSION}_linux_$(dpkg --print-architecture) --output /usr/local/bin/local-php-security-checker && \
  chmod +x /usr/local/bin/local-php-security-checker

# Pour la récupération des durées
RUN apt-get update && apt-get install -y ffmpeg

# Xdebug (disabled by default, but installed if required)
# RUN pecl install xdebug-2.9.7 && docker-php-ext-enable xdebug
# ADD xdebug.ini /usr/local/etc/php/conf.d/

WORKDIR /var/www

EXPOSE 9000

######################################################################################################################

Dans le cadre du développement de notre activité web e-Commerce, nous recherchons pour notre site de Bordeaux un(e) Ingénieur DevOps junior F/H.
Au sein d'une équipe DevOps, vous avez en charge la conception, la construction et la garantie technique des services web et e-commerce d'acteurs majeurs de l'économie numérique en France et à l'international.
Vos missions consisteront à :
•Participer à la conception et au chiffrage des solutions dans le cadre de l'avant-vente
•Construire les services et en assurer la garantie technique (disponibilité, continuité, capacité et sécurité).
•Intervenir en expertise de niveau 3 dans le cadre des opérations complexes ou sur les incidents des services de votre portefeuille
•Au sein de l'équipe, prendre en charge des missions de capitalisation des bonnes pratiques techniques ou méthodologiques, participer à la vie de l'équipe
•Conseiller nos clients sur leurs choix techniques et technologiques
•Contribuer au déploiement des pratiques DevOps au sein de l'entreprise
Dans le cadre de vos missions :
•Vous pourrez être amené(e) lors d'événements ponctuels à intervenir durant des opérations de nuit ou à assurer des astreintes de niveau 3.
•Vous pourrez être amené(e) à vous rendre ponctuellement chez nos clients.
Vous êtes diplômé(e) d'une école d'ingénieur ou êtes issue d'une formation équivalente en informatique (niveau Bac + 5).

Dans l'idéal, vous êtes à l'origine d'un SysAdmin (NetAdmin serait un plus) sur un environnement OnPremise/Datacenter outillé avec des logiciels open source.
Vous avez déjà participé au design d'infrastructures (traditionnelles et cloud-natives) et à leur mise en oeuvre, dans un contexte Web/E-commerce notamment.
Vos priorités sont la sécurité, la disponibilité, la scalabilité, et la maintenabilité.
Vous êtes intéressé(e) par la CI/CD et êtes motivé(e) par la philosophie et les pratiques DEVOPS.

Vous travaillerez dans cet environnement technique qui sera amené à évoluer:
Système : Debian, Redhat, CentOs
Virtualisation et conteneurisation : VMWare, Docker, Kubernetes
Serveurs Web : Apache, Tomcat, Nginx, IIS
Bases de données : Mysql, Oracle, SQL Server
Solutions E-commerce : Hybris, ATG
Environnements Cloud : OpenStack, Flexible Engine, Azure, AWS, GCP
Outils CI/CD : Git, Gitlab, Jenkins
Outils d'IAC : Ansible, Puppet, Salt, Terraform
Monitoring : Xymon, Prometheus

###################################################################################

Compétences techniques :

Système : Debian, Redhat, CentOs

Virtualisation et conteneurisation : VMWare, Docker, Kubernetes

Serveurs Web : Apache, Tomcat, Nginx, IIS

Bases de données : Mysql, Oracle, SQL Server

Environnements Cloud : OpenStack, Flexible Engine, Azure, AWS, GCP

Outils CI/CD : Git, Gitlab, Jenkins

Outils d'IAC : Ansible, Salt, Terraform

https://lehollandaisvolant.net/?d=2017/02/13/16/36/20-linux-rendre-le-terminal-plus-lisible

https://www.youtube.com/watch?v=kzmvwc2q_z0&list=PLn6POgpklwWoCpLKOSw3mXCqbRocnhrh-

git fetch && git reset --hard && git pull

https://www.youtube.com/watch?v=HWxBtxPBCAc&list=PLrSOXFDHBtfHg8fWBd7sKPxEmahwyVBkC

- name: Mon playbook
  hosts: all
  remote_user: admin
  vars:
    var1: "playbook"
  tasks:
  - name: Mon debug
    debug:
      msg: "{{ var1 }}"

      outils de collaboration 
      https://www.linkedin.com/learning/paths/maitriser-les-soft-skills-les-plus-demandes?trk=li-jobsindemand-softskills-fr&src=re-other&veh=www.dealabs.com

      https://www.dealabs.com/groupe/services-divers

      https://opportunity.linkedin.com/fr-fr/skills-for-in-demand-jobs

      https://opportunity.linkedin.com/fr-fr/skills-for-in-demand-jobs
