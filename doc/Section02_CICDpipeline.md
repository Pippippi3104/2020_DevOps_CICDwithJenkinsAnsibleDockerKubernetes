# CI/CD pipeline using Git, Jenkins and Maven

<a id="contents"></a>

## Contents

* [Installing Jenkins](#jenkins)
  * [1st : AWS Management Console](#jenkins_aws)
  * [2nd : java](#jenkins_java)
  * [3rd : jenkins](#jenkins_jenkins)
* [Run First Jenkins Job](#jenkins_first)
* [Git Setup](#jenkins_git)
* [Maven Setup](#jenkins_maven)
* [Run First Maven Job](#jenkins_first)

###  You can enter the Jenkins
  * [How enter Jenkins?](#jenkins_enter)
###  What is username and password of the Jenkins ?
  * [username and password of the Jenkins](#jenkins_username)
###  You can change to root@jenkins
  * [How ?](#jenkins_rootname)


<a id="jenkins"></a>

## Installing Jenkins

<a id="jenkins_aws"></a>

### 1st : AWS Management Console

* Flow of Create AWS Management Console
  * ![Image](../src/Images/Section02/aws001.png)
  * ![Image](../src/Images/Section02/aws002.png)
  * ![Image](../src/Images/Section02/aws003.png)
  * ![Image](../src/Images/Section02/aws004.png)
  * ![Image](../src/Images/Section02/aws005.png)
  * ![Image](../src/Images/Section02/aws006.png)
  * ![Image](../src/Images/Section02/aws007.png)
  * ![Image](../src/Images/Section02/aws008.png)
  * ![Image](../src/Images/Section02/aws009.png)
  * ![Image](../src/Images/Section02/aws010.png)
  * ![Image](../src/Images/Section02/aws011.png)
  * ![Image](../src/Images/Section02/aws012.png)
  * ![Image](../src/Images/Section02/aws013.png)
  * ![Image](../src/Images/Section02/aws014.png)

* How to Connect SSH?
  * [MacからAWS EC2へのSSH接続方法メモ](https://gloria.cool/blog/20200528-aws-ssh/)
    * Please run this.
      ```
      cd ~/.ssh/keys
      cp -p ダウンロードした鍵.pem ./

      chmod 600 ダウンロードした鍵.pem

      ssh EC2アカウント名@IP -i ダウンロードした鍵.pem (例: ssh ec2-user@11.11.11.11 -i key.pem)
      ```
  * [Macで公開鍵と秘密鍵を生成する方法(.sshの作成方法)](https://qiita.com/wakahara3/items/52094d476774f3a2f619)
    * Please run this if you have "/.ssh: No such file or directory".
      ```
      cd ~
      mkdir ~/.ssh
      ```
  * [SSH通信の接続と切断と終了の方法](https://www.hiramine.com/physicalcomputing/raspberrypi/ssh_connect.html)
    * Please run this.
      ```
      exit
      ```
  * Run this if you can connect AWS
    * You can change acconut like (root@ip-00-00-00-00 ~) 
      ```
      sudo su - 
      ```
    * ![Image](../src/Images/Section02/sudosu.png)

### [Return to Contents](#contents)

<a id="jenkins_java"></a>

### 2nd : java

* Flow of installing java
  * ![Image](../src/Images/Section02/java001.png)
  * ![Image](../src/Images/Section02/java002.png)
  * ![Image](../src/Images/Section02/java003.png)
  * ![Image](../src/Images/Section02/java004.png)
  * ![Image](../src/Images/Section02/java005.png)
  * ![Image](../src/Images/Section02/java006.png)

* Run these commands.
  * Install java
    ```
    yum install java-1.8*
    ```
  
  * Check it and Get the path
    ```
    find /usr/lib/jvm/java-1.8* | head -n 3
    ```
    * Then you can get the path like (/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.265.b01-1.amzn2.0.1.x86_64)
  
  * Move to .bash_profile
    ```
    cd ~
    vi .bash_profile
    ```

  * Add some text under (# User specific environment and startup programs)
    ```
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.265.b01-1.amzn2.0.1.x86_64
    PATH=$PATH:$HOME/bin:$JAVA_HOME
    ```

  * Exit .bash_profile
    ```
    :wq
    ```

  * Check tha path (you need logout onece)
    ```
    exit
    sudo su -
    echo $JAVA_HOME
    ```
    * Then you can see the path like (/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.265.b01-1.amzn2.0.1.x86_64)

### [Return to Contents](#contents)

<a id="jenkins_jenkins"></a>

### 3rd : jenkins

* Brfore installing jenkins, check setting of port 8080.
  * It you did not open prot 8080, you can not access jenkins page

* Flow of installing jenkins
  * ![Image](../src/Images/Section02/jenkins001.png)
  * ![Image](../src/Images/Section02/jenkins002.png)
  * ![Image](../src/Images/Section02/jenkins003.png)
  * ![Image](../src/Images/Section02/jenkins004.png)
  * ![Image](../src/Images/Section02/jenkins005.png)
  * ![Image](../src/Images/Section02/jenkins006.png)
  * ![Image](../src/Images/Section02/jenkins007.png)
  * ![Image](../src/Images/Section02/jenkins008.png)
  * ![Image](../src/Images/Section02/jenkins009.png)
  * ![Image](../src/Images/Section02/jenkins010.png)
  * ![Image](../src/Images/Section02/jenkins011.png)
  * ![Image](../src/Images/Section02/jenkins012.png)
  * ![Image](../src/Images/Section02/jenkins013.png)
  * ![Image](../src/Images/Section02/jenkins014.png)
  * ![Image](../src/Images/Section02/jenkins015.png)
  * ![Image](../src/Images/Section02/jenkins016.png)
  * ![Image](../src/Images/Section02/jenkins017.png)
  * ![Image](../src/Images/Section02/jenkins018.png)
  * ![Image](../src/Images/Section02/jenkins019.png)
  * ![Image](../src/Images/Section02/jenkins020.png)
  * ![Image](../src/Images/Section02/jenkins021.png)
  * ![Image](../src/Images/Section02/jenkins022.png)
  * ![Image](../src/Images/Section02/jenkins023.png)

* Run these commands.
  * Before installing jenkins, Please download this
    * [Jenkins Redhat Packages](https://pkg.jenkins.io/redhat-stable/)
    ```
    sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo

    sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
    ```

  * Install jenkins
    ```
    yum install jenkins
    ```
  
  * Then, check the jenkins service
    ```
    service jenkins start
    service jenkins status
    ```
  
  <a id="jenkins_enter"></a>
  
  <a id="jenkins_username"></a>

  * After, check at webpage
    * example) 3.14.146.56:8080
    * You need password, so run this and get password
    ```
    cat /var/lib/jenkins/secrets/initialAdminPassword
    ``` 
    * Then you have like (f632175e84a54c1dbf29a86e6f21aff3)
    * You should change your password at admin/configure (21aff3gg)
      * Next time, you can enter (ID:admin, pass:21aff3gg)
    
    * Next, you must change at manage Jenkins / Global Tool Configuration
      * JAVA_HOME
      * /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.265.b01-1.amzn2.0.1.x86_64
        * If you want to see it, run this
        ```
        echo $JAVA_HOME
        ```

### [Return to Contents](#contents)


<a id="jenkins_first"></a>

## Run First Jenkins Job

* Flow of running first jenkins job.
  * ![Image](../src/Images/Section02/first01.png)
  * ![Image](../src/Images/Section02/first02.png)
  * ![Image](../src/Images/Section02/first03.png)
  * ![Image](../src/Images/Section02/first04.png)
  * ![Image](../src/Images/Section02/first05.png)
  * ![Image](../src/Images/Section02/first06.png)
  * ![Image](../src/Images/Section02/first07.png)
  * ![Image](../src/Images/Section02/first08.png)
  * ![Image](../src/Images/Section02/first09.png)
  * ![Image](../src/Images/Section02/first10.png)

### [Return to Contents](#contents)


<a id="jenkins_git"></a>

## Git setup

* Flow of setting up the Git.
  * ![Image](../src/Images/Section02/git01.png)
  * ![Image](../src/Images/Section02/git02.png)
  * ![Image](../src/Images/Section02/git03.png)
  * ![Image](../src/Images/Section02/git04.png)
  * ![Image](../src/Images/Section02/git05.png)
  * ![Image](../src/Images/Section02/git06.png)
  * ![Image](../src/Images/Section02/git07.png)
  * ![Image](../src/Images/Section02/git08.png)
  * ![Image](../src/Images/Section02/git09.png)
  * ![Image](../src/Images/Section02/git10.png)
  * ![Image](../src/Images/Section02/git11.png)
  * ![Image](../src/Images/Section02/git12.png)

<a id="jenkins_rootname"></a>

* Run these commands.
  * enter the jenkins server.
     ```
    ssh ec2-user@3.14.146.56 -i DevOps_project.pem
    sudo su -

    hostname jenkins
    sudo su -
     ```
  * Install Git
    ```
    yum install git -y
    ```
  * Update Git Path
    * Name : github
    * path : /usr/bin/git

### [Return to Contents](#contents)


<a id="jenkins_maven"></a>

## Maven setup

* Flow of setting up the Maven.
  * ![Image](../src/Images/Section02/maven01.png)
  * ![Image](../src/Images/Section02/maven02.png)
  * ![Image](../src/Images/Section02/maven03.png)
  * ![Image](../src/Images/Section02/maven04.png)
  * ![Image](../src/Images/Section02/maven05.png)
  * ![Image](../src/Images/Section02/maven06.png)
  * ![Image](../src/Images/Section02/maven07.png)
  * ![Image](../src/Images/Section02/maven08.png)
  * ![Image](../src/Images/Section02/maven09.png)
  * ![Image](../src/Images/Section02/maven10.png)
  * ![Image](../src/Images/Section02/maven11.png)
  * ![Image](../src/Images/Section02/maven12.png)
  * ![Image](../src/Images/Section02/maven13.png)

* Run these commends.
  * Installing Maven
    ```
    pwd
    cd /opt
    ls -ltr

    wget https://ftp.riken.jp/net/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.tar.gz
    ```
  * Make folder
    ```
    tar -xvzf apache-maven-3.6.3-bin.tar.gz
    mv apache-maven-3.6.3 maven
    cd maven
    pwd
    ```
  * enter bash_profile
    ```
    vi ~/.bash_profile
    ```
  * Uptate bash_profile
    ```
    JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.265.b01-1.amzn2.0.1.x86_64
    M2_HOME=/opt/maven
    M2=/opt/maven/bin
    PATH=$PATH:$HOME/bin:$JAVA_HOME:$M2:$M2_HOME
    ```
    * Check at [Downloading Apache Maven](https://maven.apache.org/download.cgi)

  * Check the M2 path
    ```
    exit
    sudo su -
    echo $M2
    mvn --version
    ```
    * Then you can get like (/opt/maven/bin) and (Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
      Maven home: /opt/maven
      Java version: 1.8.0_265, vendor: Oracle Corporation, runtime: /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.265.b01-1.amzn2.0.1.x86_64/jre
      Default locale: en_US, platform encoding: UTF-8
      OS name: "linux", version: "4.14.203-156.332.amzn2.x86_64", arch: "amd64", family: "unix")

### [Return to Contents](#contents)


<a id="maven_first"></a>

## Run First Maven Job

* Flow of running first maven job.
  * ![Image](../src/Images/Section02/firstmaven01.png)
  * ![Image](../src/Images/Section02/firstmaven02.png)
  * ![Image](../src/Images/Section02/firstmaven03.png)
  * ![Image](../src/Images/Section02/firstmaven04.png)
  * ![Image](../src/Images/Section02/firstmaven05.png)
  * ![Image](../src/Images/Section02/firstmaven06.png)
  * ![Image](../src/Images/Section02/firstmaven07.png)
  * ![Image](../src/Images/Section02/firstmaven08.png)
  * ![Image](../src/Images/Section02/firstmaven09.png)
  * ![Image](../src/Images/Section02/firstmaven10.png)
  * ![Image](../src/Images/Section02/firstmaven11.png)

* Before running, check the git repository.
  * https://github.com/yankils/hello-world.git
  * You must check repository name. master? or main? or ,,,,

* After running first job, Please check workspace
  ```
  cd /var/lib/jenkins/workspace/
  ls
  ```
  * you can get (My_First_Job  My_First_Maven_Build)
  ```
  cd My_First_Maven_Job
  ls
  cd webapp/target/
  ls
  ```

### [Return to Contents](#contents)






