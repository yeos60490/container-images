FROM centos:7.6.1810

ENV container docker
#ENV LC_ALL=C.UTF-8

#install systemctl 
RUN yum -y update; yum clean all
RUN yum -y install systemd; yum clean all; \
        (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == systemd-tmpfiles-setup.service ] || rm -f $i; done); \
        rm -f /lib/systemd/system/multi-user.target.wants/*;\
        rm -f /etc/systemd/system/*.wants/*;\
        rm -f /lib/systemd/system/local-fs.target.wants/*; \
        rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
        rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
        rm -f /lib/systemd/system/basic.target.wants/*;\
        rm -f /lib/systemd/system/anaconda.target.wants/*;


#install httpd
RUN yum -y install httpd; \
        yum clean all;  \
        systemctl enable httpd.service;


RUN yum -y install git

#install php7.3
RUN yum -y install wget; \
        wget https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm; \
        wget http://rpms.remirepo.net/enterprise/remi-release-7.rpm; \
        rpm -Uvh remi-release-7.rpm epel-release-latest-7.noarch.rpm; \
        yum-config-manager --enable remi-php73; \
        yum install -y php php-common php-opcache php-mcrypt php-cli php-gd php-curl php-mysql -y;


RUN yum install -y vim; \
        yum install -y R; \
        localedef -f UTF-8 -i ko_KR ko_KR.UTF-8;


VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]
CMD ["/usr/sbin/httpd", "-D", "FOREGROUND"]
