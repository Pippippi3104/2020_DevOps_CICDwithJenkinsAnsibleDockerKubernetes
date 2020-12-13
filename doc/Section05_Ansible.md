# Integrating Ansible in CI/CD pipeline

<a id="contents"></a>

## Contents

* [Ansible Setup](#ansible_set)
* [Integrating Ansible with Jenkins](#ansible_jen)

### Trouble
* 


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
  /Password
  ```
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





