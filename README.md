## Centos 기반 WAS 컨테이너 이미지

------

기본 이미지는 dockerhub 에서 제공하는 centos:7.6.1810 를 사용 (https://hub.docker.com/_/centos)    
추가적으로 php, apache 등을 설치하여 웹 서버를 실행하도록 환경설정 및 컨테이너 권한 부여  

------

- 구성환경

>  centos 7 \
    apache2 \
    php 7.3 \
    git \
    vim \
    locale

- image build 방법 (Dockerfile 이 있는 경로에서)

        docker build -t {이미지이름}:{이미지태그} .
    
- container 구동

        docker run --name {컨테이너이름} --privileged --cap-add=NET_ADMIN -tid -p 80:80 -e container=docker -v /sys/fs/cgroup:/sys/fs/cgroup {이미지이름}:{태그} /usr/sbin/init
    

------



------
### 환경설치 (OS: centos7)
#### docker
- 먼저 설치되어 있으면 지우기 

      sudo yum remove docker \ 
                docker-client \
                docker-client-latest \
                docker-common \
                docker-latest \
                docker-latest-logrotate \
                docker-logrotate \
                docker-selinux \
                docker-engine-selinux \
                docker-engine
                
- 설치 
  
      sudo yum install yum-utils device-mapper-persistent-data lvm2
      sudo yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
      sudo yum install docker-ce-19.03.13
      
- 실행

      sudo systemctl start docker
      sudo systemctl status docker
      sudo systemctl enable docker
      
#### docker-compose

- 설치
      
      sudo curl -L "https://github.com/docker/compose/releases/download/1.27.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
      sudo chmod +x /usr/local/bin/docker-compose
      sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
      
- 설치 확인

      docker-compose --version  
