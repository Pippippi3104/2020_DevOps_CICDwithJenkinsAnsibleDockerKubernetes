# Integration Kubernets in CI/CD pipeline

<a id="contents"></a>

## Contents

* [Introduction to Kubernets Section](#kubernets_intro)
* [Setup Kubernetes Part1 - Setup Ubuntu Server](#kubernets_ubuntu)

### Trouble
* [シンボリックリンクを作成する](https://www.atmarkit.co.jp/ait/articles/1605/30/news022.html)
  * make python using python3
    * [Ubuntu 18.04でPoetryを動かしてみる。](https://qiita.com/sabaku20XX/items/6147432996fccc335568)


<a id="kubernets_intro"></a>

## Introduction to Kubernets Section

* Introducing Kubernetes
  * Setting up Kubernetes environment
  * Using Kubectl commands
  * Writing deployment and service files
  * Creating Ansible Playbooks to deploy
  * Run a jenkins job

* Flow
  * ![Image](../src/Images/Section06/intro001.png)
  * ![Image](../src/Images/Section06/intro002.png)
  * ![Image](../src/Images/Section06/intro003.png)
  * ![Image](../src/Images/Section06/intro004.png)

* commands

### [Return to Contents](#contents)


* [Setup Kubernetes Part1 - Setup Ubuntu Server](#kubernets_ubuntu)
<a id="kubernets_ubuntu"></a>

## Setup Kubernetes Part1 - Setup Ubuntu Server

* Flow
  * ![Image](../src/Images/Section06/ubuntu001.png)
  * ![Image](../src/Images/Section06/ubuntu002.png)
  * ![Image](../src/Images/Section06/ubuntu003.png)
  * ![Image](../src/Images/Section06/ubuntu004.png)
  * ![Image](../src/Images/Section06/ubuntu005.png)
  * ![Image](../src/Images/Section06/ubuntu006.png)
  * ![Image](../src/Images/Section06/ubuntu007.png)
  * ![Image](../src/Images/Section06/ubuntu008.png)
  * ![Image](../src/Images/Section06/ubuntu009.png)
  * ![Image](../src/Images/Section06/ubuntu010.png)
  * ![Image](../src/Images/Section06/ubuntu011.png)
  * ![Image](../src/Images/Section06/ubuntu012.png)
  * ![Image](../src/Images/Section06/ubuntu013.png)
  * ![Image](../src/Images/Section06/ubuntu014.png)
  * ![Image](../src/Images/Section06/ubuntu015.png)
  * ![Image](../src/Images/Section06/ubuntu016.png)
  * ![Image](../src/Images/Section06/ubuntu017.png)
  * ![Image](../src/Images/Section06/ubuntu018.png)
  * ![Image](../src/Images/Section06/ubuntu019.png)
  * ![Image](../src/Images/Section06/ubuntu020.png)
  * ![Image](../src/Images/Section06/ubuntu021.png)
  * ![Image](../src/Images/Section06/ubuntu022.png)

* commands
  * work at ubuntu
  ```
  cd ~/.ssh/keys
  cp -p ダウンロードした鍵.pem ./
  chmod 600 ダウンロードした鍵.pem

  ssh ubuntu@3.14.150.81 -i DevOps_project.pem
  ```
  ```
  sudo su -
  curl https://s3.amazonaws.com/aws-cli/awscli-bundle.zip -o awscli-bundle.zip
  ls
  apt install unzip python3

  cd /usr/bin/
  ln -s /usr/bin/python3 ./python
  
  sudo apt update
  sudo apt upgrade

  unzip awscli-bundle.zip
  sudo apt-get install python3-venv
  ./awscli-bundle/install -i /usr/local/aws -b /usr/local/bin/aws
  aws --version
  ```
  ```
  curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
  ls -l
  chmod +x ./kubectl 

  sudo mv ./kubectl /usr/local/bin/kubectl
  kubectl
  ```
  ```
   curl -LO https://github.com/kubernetes/kops/releases/download/$(curl -s https://api.github.com/repos/kubernetes/kops/releases/latest | grep tag_name | cut -d '"' -f 4)/kops-linux-amd64
   chmod +x kops-linux-amd64
   sudo mv kops-linux-amd64 /usr/local/bin/kops
   kops
  ```

### [Return to Contents](#contents)




