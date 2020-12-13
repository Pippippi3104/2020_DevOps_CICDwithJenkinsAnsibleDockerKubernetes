# Integrating Docker in CI/CD Pipeline

<a id="contents"></a>

## Contents

* [Docker Setup](#docker_set)
* [Docker*Tomcat Image Issue](#docker_iss)
* [Integrating DockerHost With Jenkins](#docker_jen)
* [Jenkins Job to Copy Artifactson to DockerHost](#docker_job)
* [Create a Dockerfile](#docker_file)

### Trouble
* If you want open port XXXX, check [this](https://forums.aws.amazon.com/thread.jspa?threadID=307722)


<a id="docker_set"></a>

## Docker Setup

* Flow of Setup Docker
  * ![Image](../src/Images/Section04/setup001.png)
  * ![Image](../src/Images/Section04/setup002.png)
  * ![Image](../src/Images/Section04/setup003.png)
  * ![Image](../src/Images/Section04/setup004.png)
  * ![Image](../src/Images/Section04/setup005.png)
  * ![Image](../src/Images/Section04/setup006.png)
  * ![Image](../src/Images/Section04/setup007.png)
  * ![Image](../src/Images/Section04/setup008.png)
  * ![Image](../src/Images/Section04/setup009.png)
  * ![Image](../src/Images/Section04/setup010.png)
  * ![Image](../src/Images/Section04/setup011.png)
  * ![Image](../src/Images/Section04/setup012.png)
  * ![Image](../src/Images/Section04/setup013.png)
  * ![Image](../src/Images/Section04/setup014.png)
  * ![Image](../src/Images/Section04/setup015.png)
  * ![Image](../src/Images/Section04/setup016.png)
  * ![Image](../src/Images/Section04/setup017.png)
  * ![Image](../src/Images/Section04/setup018.png)
  * ![Image](../src/Images/Section04/setup019.png)
  * ![Image](../src/Images/Section04/setup020.png)
  * ![Image](../src/Images/Section04/setup021.png)
  * ![Image](../src/Images/Section04/setup022.png)
  * ![Image](../src/Images/Section04/setup023.png)
  * ![Image](../src/Images/Section04/setup024.png)
  * ![Image](../src/Images/Section04/setup025.png)
  * ![Image](../src/Images/Section04/setup026.png)

* Run these commands
  ```
  hostname docker-host
  sudo su -
  yum install docker
  ```
  ```
  service docker start
  service docker status
  docker ps
  ```
  * check this page
    * https://hub.docker.com/
    * Search Tomcat
  * Image
  ```
  docker image ls
  docker pull tomcat:latest
  docker images
  docker run --name tomcat-container -p 8080:8080 tomcat:latest
  ``` 
  * You can't open tomcat page, but you will be able to open after next lesson.
  ```
  docker ps
  docker ps -a
  docker rm 2ef49f6c14a7
  docker run --name tomcat-container -p 8080:8080 tomcat:latest
  ```

### [Return to Contents](#contents)


<a id="docker_iss"></a>

## Docker * Tomcat Image issue

* Flow
  * ![Image](../src/Images/Section04/iss001.png)
  * ![Image](../src/Images/Section04/iss002.png)
  * ![Image](../src/Images/Section04/iss003.png)
  * ![Image](../src/Images/Section04/iss004.png)
  * ![Image](../src/Images/Section04/iss005.png)
  * ![Image](../src/Images/Section04/iss006.png)
  * ![Image](../src/Images/Section04/iss007.png)
  * ![Image](../src/Images/Section04/iss008.png)
  * ![Image](../src/Images/Section04/iss009.png)
  * ![Image](../src/Images/Section04/iss010.png)

* Commands
  * open tomcat page
  ```
  docker images
  docker ps -a
  docker rm 58ee54e9dcd3
  ```
  ```
  docker run -d --name tomcat-container -p 8080:8080 tomcat
  docker ps -a
  ```
  ```
  docker exec -it tomcat-container /bin/bash
  ls
  cd webapps
  ls
  cd ..
  cd webapps.dist/
  ls
  ```
  ```
  cp -R * ../webapps
  cd ../webapps
  ls
  exit
  ```
  * check docker page
    * https://hub.docker.com/_/tomcat
  ```
  docker images
  docker pull tomcat:8.0
  docker images
  ```
  * run another tomcat
    * You must need open port 8081
  ```
  docker run -d --name tomcat-8 -p 8081:8080 tomcat:8.0
  docker ps -a
  ```
  * If you want restart docker container, run this
  ```
  docker restart b6fe1e5b8656 
  ```

### [Return to Contents](#contents)


<a id="docker_jen"></a>

## Integrating DockerHost With Jenkins

* Flow
  * ![Image](../src/Images/Section04/jen001.png)
  * ![Image](../src/Images/Section04/jen002.png)
  * ![Image](../src/Images/Section04/jen003.png)
  * ![Image](../src/Images/Section04/jen004.png)
  * ![Image](../src/Images/Section04/jen005.png)
  * ![Image](../src/Images/Section04/jen006.png)
  * ![Image](../src/Images/Section04/jen007.png)
  * ![Image](../src/Images/Section04/jen008.png)
  * ![Image](../src/Images/Section04/jen009.png)
  * ![Image](../src/Images/Section04/jen010.png)
  * ![Image](../src/Images/Section04/jen011.png)
  * ![Image](../src/Images/Section04/jen012.png)
  * ![Image](../src/Images/Section04/jen013.png)
  * ![Image](../src/Images/Section04/jen014.png)
  * ![Image](../src/Images/Section04/jen015.png)
  * ![Image](../src/Images/Section04/jen016.png)
  * ![Image](../src/Images/Section04/jen017.png)
  * ![Image](../src/Images/Section04/jen018.png)

* Commands
  * use docker-host
  ```
  useradd dockeradmin
  passwd dockeradmin
  ```
  * pass : 21aff3gg
  ```
  cat /etc/group
  usermod -aG docker dockeradmin
  id dockeradmin
  ```
  * check the path
  ```
  pi addr
  vi /etc/ssh/sshd_config
  service sshd reload
  ```

### [Return to Contents](#contents)


<a id="docker_job"></a>

## Jenkins Job to Copy Artifactson to DockerHost

* Flow
  * ![Image](../src/Images/Section04/job001.png)
  * ![Image](../src/Images/Section04/job002.png)
  * ![Image](../src/Images/Section04/job003.png)
  * ![Image](../src/Images/Section04/job004.png)
  * ![Image](../src/Images/Section04/job005.png)
  * ![Image](../src/Images/Section04/job006.png)
  * ![Image](../src/Images/Section04/job007.png)
  * ![Image](../src/Images/Section04/job008.png)
  * ![Image](../src/Images/Section04/job009.png)
  * ![Image](../src/Images/Section04/job010.png)
  * ![Image](../src/Images/Section04/job011.png)
  * ![Image](../src/Images/Section04/job012.png)
  * ![Image](../src/Images/Section04/job013.png)
  * ![Image](../src/Images/Section04/job014.png)
  * ![Image](../src/Images/Section04/job015.png)
  * ![Image](../src/Images/Section04/job016.png)
  * ![Image](../src/Images/Section04/job017.png)
  * ![Image](../src/Images/Section04/job018.png)

* Commands
  * work at jenkins
  ```
  cd /var/lib/jenkins/workspace
  pwd
  ls
  cd Deploy_on_Tomcat_Server/
  ls
  cd webapp/
  ls
  cd target
  pwd
  ```
  * work at docker-host
  ```
  cd /home/dockeradmin
  su - dockeradmin
  pwd
  whoami
  ```
  ```
  cd webapp/target/
  ls
  pwd
  ```
  ```
  cd ..
  cd ~
  ls
  rm -rf webapp/
  ```
  * build again, then check
  ```
  ls
  pwd
  ```

### [Return to Contents](#contents)


<a id="docker_file"></a>

## Create a Dockerfile

* Flow
  * ![Image](../src/Images/Section04/file001.png)

* Commands
  * work at dockeradmin
  ```
  su - dockeradmin
  ls
  vi Dockerfile
  ```
  * write at Dockerfile
  ```
  FROM tomcat:latest

  MAINTAINER AR Shankar

  COPY ./webapp.war /usr/local/tomcat/webapps
  ```
  * work at dockeradmin
  ```
  docker ps
  ls
  docker build -t devops-project .
  docker images
  docker run --name devops-container -p 8080:8080 devops-project
  ```
  ```
  docker ps -a
  docker rm 52ea2d02d244
  docker run -d --name devops-container -p 8080:8080 devops-project
  ```

### [Return to Contents](#contents)


