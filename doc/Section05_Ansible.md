# Integrating Ansible in CI/CD pipeline

<a id="contents"></a>

## Contents

* [Ansible Setup](#ansible_set)
* [Integrating Ansible with Jenkins](#ansible_jen)
* [Creating an Ansible Playbook](#ansible_book)
* [Common issue faced during practice](#ansible_iss)
* [Run Ansible Playbook From Jenkins](#ansible_run)
  * Still have problem !
    * always stop auto building !
* [Update Ansible Playbook to Delete and Create Docker Container](#andible_update)
* [DockerHub Integration with Ansible](#ansible_dochub)
* [Tagging Docker Image Using Ansible Playbooks](#ansible_tag)
* [Jenkins job to deploy on Docker container through DOckerfile](#andsible_jobdoc)

### Trouble
* Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
  * Run these commands
  ```
  service docker status
  sudo service docker start
  ```
  * [WSL上でDockerを動かす際に躓いたこと](https://qiita.com/neight0903/items/ef0e2170b712b194c3fc)


<a id="ansible_set"></a>

## Ansible Setup

* Flow
  * ![Image](../src/Images/Section05/setup001.png)
  * ![Image](../src/Images/Section05/setup002.png)
  * ![Image](../src/Images/Section05/setup003.png)
  * ![Image](../src/Images/Section05/setup004.png)
  * ![Image](../src/Images/Section05/setup005.png)
  * ![Image](../src/Images/Section05/setup006.png)
  * ![Image](../src/Images/Section05/setup007.png)
  * ![Image](../src/Images/Section05/setup008.png)
  * ![Image](../src/Images/Section05/setup009.png)
  * ![Image](../src/Images/Section05/setup010.png)
  * ![Image](../src/Images/Section05/setup011.png)
  * ![Image](../src/Images/Section05/setup012.png)
  * ![Image](../src/Images/Section05/setup013.png)
  * ![Image](../src/Images/Section05/setup014.png)
  * ![Image](../src/Images/Section05/setup015.png)
  * ![Image](../src/Images/Section05/setup016.png)
  * ![Image](../src/Images/Section05/setup017.png)
  * ![Image](../src/Images/Section05/setup018.png)
  * ![Image](../src/Images/Section05/setup019.png)
  * ![Image](../src/Images/Section05/setup020.png)
  * ![Image](../src/Images/Section05/setup021.png)
  * ![Image](../src/Images/Section05/setup022.png)
  * ![Image](../src/Images/Section05/setup023.png)
  * ![Image](../src/Images/Section05/setup024.png)
  * ![Image](../src/Images/Section05/setup025.png)
  * ![Image](../src/Images/Section05/setup026.png)
  * ![Image](../src/Images/Section05/setup027.png)
  * ![Image](../src/Images/Section05/setup028.png)
  * ![Image](../src/Images/Section05/setup029.png)
  * ![Image](../src/Images/Section05/setup030.png)
  * ![Image](../src/Images/Section05/setup031.png)
  * ![Image](../src/Images/Section05/setup032.png)
  * ![Image](../src/Images/Section05/setup033.png)
  * ![Image](../src/Images/Section05/setup034.png)
  * ![Image](../src/Images/Section05/setup035.png)
  * ![Image](../src/Images/Section05/setup036.png)
  * ![Image](../src/Images/Section05/setup037.png)
  * ![Image](../src/Images/Section05/setup038.png)
  * ![Image](../src/Images/Section05/setup039.png)
  * ![Image](../src/Images/Section05/setup040.png)
  * ![Image](../src/Images/Section05/setup041.png)

* commands
  * work at ansible
  ```
  ssh ec2-user@18.222.204.55 -i DevOps_project.pem
  sudo su -
  yum install python
  python --version
  ```
  ```
  yum install python-pip
  pip install ansible
  ansible --version
  ```
  ```
  mkdir /etc/ansible
  useradd ansadmin
  passwd ansadmin
  ```
  * pass : 21aff3gg
  ```
  visudo
  ansadmin ALL=(ALL)       NOPASSWD: ALL
  ```
  ```
  yum install docker
  service docker status
  service docker start
  ```
  ```
  usermod -aG docker ansadmin
  vi /etc/ssh/sshd_config
  ```
  * using '/Password' then you can access 
  * no → yes
  ```
  service sshd reload
  su - ansadmin
  ssh-keygen
  ```
  ```
  ls -la
  cd .ssh
  ls
  cd ..
  exit
  hostname ansible-control-node
  sudo su -
  ```
  * work at docker-host
  ```
  useradd ansadmin
  passwd ansadmin
  ```
  * pass : 21aff3gg
  ```
  ip addr
  ```
  * work at ansadmin
  ```
  su - ansadmin
  ssh-copy-id ansadmin@172.31.2.113
  ```
  * pass : 21aff3gg
  ```
  ssh ansadmin@172.31.2.113
  exit
  cd /etc/ansible
  ls
  sudo vi hosts
  ```
  ```
  172.31.2.113
  localhost
  ```
  ```
  ansible all -m ping
  ssh-copy-id localhost
  ansible all -m ping
  ```
  * pass: 21aff3gg

### [Return to Contents](#contents)


<a id="ansible_jen"></a>

## Integrating Ansible with Jenkins

* Flow
  * ![Image](../src/Images/Section05/jen001.png)
  * ![Image](../src/Images/Section05/jen002.png)
  * ![Image](../src/Images/Section05/jen003.png)
  * ![Image](../src/Images/Section05/jen004.png)
  * ![Image](../src/Images/Section05/jen005.png)
  * ![Image](../src/Images/Section05/jen006.png)
  * ![Image](../src/Images/Section05/jen007.png)
  * ![Image](../src/Images/Section05/jen008.png)
  * ![Image](../src/Images/Section05/jen009.png)
  * ![Image](../src/Images/Section05/jen010.png)
  * ![Image](../src/Images/Section05/jen011.png)
  * ![Image](../src/Images/Section05/jen012.png)
  * ![Image](../src/Images/Section05/jen013.png)
  * ![Image](../src/Images/Section05/jen014.png)

* commands
  * work at ansible-control-node
  ```
  ip addr
  ```
  * pass: 21aff3gg
  ```
  cd /opt
  sudo mkdir docker
  sudo chown -R ansadmin:ansadmin /opt/docker
  ls -l /opt
  ```
  ```
  cd docker
  ls -l
  pwd
  ```
  * You can see the file 'webapp.war' after building
  ```
  ls
  ```

### [Return to Contents](#contents)


<a id="ansible_book"></a>

## Creating an Ansible Playbook

* Flow
  * ![Image](../src/Images/Section05/book001.png)
  * ![Image](../src/Images/Section05/book002.png)
  * ![Image](../src/Images/Section05/book003.png)
  * ![Image](../src/Images/Section05/book004.png)
  * ![Image](../src/Images/Section05/book005.png)
  * ![Image](../src/Images/Section05/book006.png)
  * ![Image](../src/Images/Section05/book007.png)
  * ![Image](../src/Images/Section05/book008.png)
  * ![Image](../src/Images/Section05/book009.png)
  * ![Image](../src/Images/Section05/book010.png)
  * ![Image](../src/Images/Section05/book011.png)
  * ![Image](../src/Images/Section05/book012.png)
  * ![Image](../src/Images/Section05/book013.png)

* commands
  * work at ansible, (ansible-control-node docker)
  ```
  su - ansadmin
  cd /opt/docker
  ls
  pwd
  ```
  * work at docker-host
  ```
  cd /home/dockeradmin/
  ls
  cat Dockerfile
  ```
  * work at ansible
  ```
  vi Dockerfile
  FROM tomcat:latest
  
  MAINTAINER AR Shankar

  COPY ./webapp.war /usr/local/tomcat/webapps
  ```
  * [Ansibleのローカル実行(ansible-playが動かない時)](https://qiita.com/hiroyuki_onodera/items/e6d0d308eb44e26fa03f)
  ```
  vi simple-devops-image.yml
  ---
  - hosts: localhost
    become: true
  
    tasks:
    - name: build docker image using war file
      command: docker build -t simple-devops-image .
      args:
        chdir: /opt/docker
  ```
  ```
  docker images
  docker ps -a
  ls
  cat /etc/ansible/hosts
  cat simple-devops-image.yml
  ansible-playbook -i hosts simple-devops-image.yml --check
  ansible-playbook -i hosts simple-devops-image.yml
  docker images
  ```
  ```
  ---
  vi simple-devops-image.yml
  - hosts: localhost
    become: true

    tasks:
    - name: build docker image using war file
      command: docker build -t simple-devops-image .
      args:
        chdir: /opt/docker

    - name: create container using simple-devops-image
      command: docker run -d --name simple-devops-container -p 8080:8080 simple-devops-image
  ```
  ```
  mv simple-devops-image.yml simple-devops-project.yml
  ansible-playbook -i hosts simple-devops-project.yml
  docker images
  docker ps -a
  ```
  * You can open tomcat page if you run these
  ```
  docker exec -it simple-devops-container /bin/bash
  cd webapps.dist/
  cp -R * ../webapps
  cd ../webapps
  ```

### [Return to Contents](#contents)


<a id="ansible_iss"></a>

## Common issue faced during practice

* Flow
  * ![Image](../src/Images/Section05/iss001.png)
  * ![Image](../src/Images/Section05/iss002.png)
  * ![Image](../src/Images/Section05/iss003.png)
  * ![Image](../src/Images/Section05/iss004.png)
  * ![Image](../src/Images/Section05/iss005.png)
  * ![Image](../src/Images/Section05/iss006.png)

* commands

### [Return to Contents](#contents)


<a id="ansible_run"></a>

## Run Ansible Playbook From Jenkins

* Flow
  * ![Image](../src/Images/Section05/run001.png)
  * ![Image](../src/Images/Section05/run002.png)
  * ![Image](../src/Images/Section05/run003.png)
  * ![Image](../src/Images/Section05/run004.png)
  * ![Image](../src/Images/Section05/run005.png)
  * ![Image](../src/Images/Section05/run006.png)
  * ![Image](../src/Images/Section05/run007.png)
  * ![Image](../src/Images/Section05/run008.png)
  * ![Image](../src/Images/Section05/run009.png)
  * ![Image](../src/Images/Section05/run010.png)
  * ![Image](../src/Images/Section05/run011.png)
  * ![Image](../src/Images/Section05/run012.png)
  * ![Image](../src/Images/Section05/run013.png)
  * ![Image](../src/Images/Section05/run014.png)

* commands
  * work at ansible-control-node docker
  ```
  cd /opt/docker
  pwd
  docker images
  docker ps -a
  ```
  ```
  docker stop 7fd2258f8f4f
  docker rm 7fd2258f8f4f
  docker rmi simple-devops-image tomcat
  docker images
  docker ps -a
  ```
  * write at Exec command
  ```
  ansible-playbook -i /opt/docker/hosts /opt/docker/simple-devops-project.yml;
  ```
  * work at ansible-control-node docker
  ```
  docker images
  docker ps -a
  ```
  * You can open tomcat page if you run these
  ```
  docker exec -it simple-devops-container /bin/bash
  cd webapps.dist/
  cp -R * ../webapps
  cd ../webapps
  ```
  * work at jenkins
  ```
  ls
  cd hello-world/
  ls
  git pull
  vi webapp/src/main/webapp/index.jsp
  <h2> Deploying on a container </h2>
  ```
  ```
  git status
  git add .
  git commit -m "modified index file to test with docker"
  git push
  ```
  * you can use if you want to merge
  ```
  git merge --abort
  ```

### [Return to Contents](#contents)


<a id="andible_update"></a>

## Update Ansible Playbook to Delete and Create Docker Container

* Flow
  * ![Image](../src/Images/Section05/update001.png)
  * ![Image](../src/Images/Section05/update002.png)
  * ![Image](../src/Images/Section05/update003.png)
  * ![Image](../src/Images/Section05/update004.png)
  * ![Image](../src/Images/Section05/update005.png)
  * ![Image](../src/Images/Section05/update006.png)
  * ![Image](../src/Images/Section05/update007.png)
  * ![Image](../src/Images/Section05/update008.png)
  * ![Image](../src/Images/Section05/update009.png)

* commands
  * work at ansible-contorol-node
  ```
  cd /opt/docker
  pwd
  vi simple-devops-project.yml
  ```
  ```
  - name: stop current running container
    command: docker stop simple-devops-container
    ignore_errors: yes

  - name: remove stopped container
    command: docker rm simple-devops-container
    ignore_errors: yes

  - name: remove docker image
    command: docker rmi simple-devops-image
    ignore_errors: yes
  ```
  ```
  cat simple-devops-project.yml
  ```
  * after building,,,
  ```
  docker images
  docker ps -a
  ```
  ```
  docker exec -it simple-devops-container /bin/bash
  cd webapps.dist/
  cp -R * ../webapps
  cd ../webapps
  ```
  * work at jenkins hello-world
  ```
  vi webapp/src/main/webapp/index.jsp
  git status
  git add .
  git commit -m "modified index file to test with docker"
  git push
  ```

### [Return to Contents](#contents)


<a id="ansible_dochub"></a>

## DockerHub Integration with Ansible

* Make your account
  * [Docker Hub](https://hub.docker.com/)

* Flow
  * ![Image](../src/Images/Section05/dochub001.png)
  * ![Image](../src/Images/Section05/dochub002.png)
  * ![Image](../src/Images/Section05/dochub003.png)
  * ![Image](../src/Images/Section05/dochub004.png)
  * ![Image](../src/Images/Section05/dochub005.png)
  * ![Image](../src/Images/Section05/dochub006.png)
  * ![Image](../src/Images/Section05/dochub007.png)
  * ![Image](../src/Images/Section05/dochub008.png)
  * ![Image](../src/Images/Section05/dochub009.png)
  * ![Image](../src/Images/Section05/dochub010.png)
  * ![Image](../src/Images/Section05/dochub011.png)
  * ![Image](../src/Images/Section05/dochub012.png)
  * ![Image](../src/Images/Section05/dochub013.png)
  * ![Image](../src/Images/Section05/dochub014.png)

* commands
  * work at ansible-contorol-node
  ```
  cd /opt/docker
  docker images
  docker tag simple-devops-image pippippi/simple-devops-image
  docker push pippippi/simple-devops-image
  ```
  ```
  docker login (pippippi)
  docker push
  docker rmi pippippi/simple-devops-image
  docker pull pippippi/simple-devops-image
  ```
  * work at docker-host
  ```
  su - ansadmin
  id
  eixt
  usermod -aG docker ansadmin
  id
  ```
  ```
  docker images
  docker pull pippippi/simple-devops-image
  docker images
  ```

### [Return to Contents](#contents)


<a id="ansible_tag"></a>

## Tagging Docker Image Using Ansible Playbooks

* Flow
  * ![Image](../src/Images/Section05/tag001.png)
  * ![Image](../src/Images/Section05/tag002.png)
  * ![Image](../src/Images/Section05/tag003.png)
  * ![Image](../src/Images/Section05/tag004.png)
  * ![Image](../src/Images/Section05/tag005.png)
  * ![Image](../src/Images/Section05/tag006.png)
  * ![Image](../src/Images/Section05/tag007.png)
  * ![Image](../src/Images/Section05/tag008.png)
  * ![Image](../src/Images/Section05/tag009.png)
  * ![Image](../src/Images/Section05/tag010.png)
  * ![Image](../src/Images/Section05/tag011.png)
  * ![Image](../src/Images/Section05/tag012.png)
  * ![Image](../src/Images/Section05/tag013.png)
  * ![Image](../src/Images/Section05/tag014.png)

* commands
  * work at ansible-control-node docker
  ```
  pwd (/opt/docker)
  ls
  vi create-simple-devops-image.yml
  ```
  ```
  ---
  - hosts: localhost
    become: true
    
    tasks:
    - name: create docker image using war file
      command: docker build -t simple-devops-image:latest .
      args:
        chdir: /opt/docker
        
    - name: create tag to image
      command: docker tag simple-devops-image pippippi/simple-devops-image
      
    - name: push image on to dockerhub
      command: docker push pippippi/simple-devops-image
      
    - name: remove docker images from ansible server
      command: docker rmi simple-devops-image:latest pippippi/simple-devops-image
      ignore_errors: yes
  ```
  ```
  ls
  ansible-playbook -i hosts create-simple-devops-image.yml
  docker images
  docker ps -a
  docker rm -f cf62d49d16de
  docker rmi pippippi/simple-devops-image
  cat hosts
  ansible-playbook -i hosts create-simple-devops-image.yml
  docker images
  docker ps -a
  ```
  ```
  vi create-simple-devops-project.yml
  ---
  - hosts: localhost
    become: true

    tasks:
    - name: stop current running container
      command: docker stop simple-devops-container
      ignore_errors: yes

    - name: remove stopped container
      command: docker rm simple-devops-container
      ignore_errors: yes

    - name: remove docker image
      command: docker rmi pippippi/simple-devops-image:latest
      ignore_errors: yes

    - name: pull docker image from dockerhub
      command: docker pull pippippi/simple-devops-image:latest

    - name: craete container using simple-devops-image
      command: docker run -d --name simple-devops-container -p 8080:8080 pippippi/simple-devops-image:latest
  ```
  ```
  ansible-playbook -i hosts create-simple-devops-project.yml
  ```

### [Return to Contents](#contents)


<a id="andsible_jobdoc"></a>

## Jenkins job to deploy on Docker container through DOckerfile

* commands
  * work at ansible-control-node docker
  ```
  cd ~/.ssh/keys
  cp -p ダウンロードした鍵.pem ./

  chmod 600 ダウンロードした鍵.pem

  ssh EC2アカウント名@IP -i ダウンロードした鍵.pem (例: ssh ec2-user@11.11.11.11 -i key.pem)
  ```
  ```
  pwd
  ls
  cat create-simple-devops-image.yml
  cat create-simple-devops-project.yml
  cat hosts
  ```

### [Return to Contents](#contents)





