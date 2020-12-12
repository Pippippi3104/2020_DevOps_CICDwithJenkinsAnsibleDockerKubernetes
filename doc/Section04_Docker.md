# Integrating Docker in CI/CD Pipeline

<a id="contents"></a>

## Contents

* [Docker Setup](#docker_set)
* [Docker*Tomcat Image Issue](#docker_iss)

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


