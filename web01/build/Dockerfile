FROM centos:7.4.1708

ENV container docker
RUN (cd /lib/systemd/system/sysinit.target.wants/; for i in *; do [ $i == \
systemd-tmpfiles-setup.service ] || rm -f $i; done); \
rm -f /lib/systemd/system/multi-user.target.wants/*;\
rm -f /etc/systemd/system/*.wants/*;\
rm -f /lib/systemd/system/local-fs.target.wants/*; \
rm -f /lib/systemd/system/sockets.target.wants/*udev*; \
rm -f /lib/systemd/system/sockets.target.wants/*initctl*; \
rm -f /lib/systemd/system/basic.target.wants/*;\
rm -f /lib/systemd/system/anaconda.target.wants/*;
VOLUME [ "/sys/fs/cgroup" ]
CMD ["/usr/sbin/init"]

###RUN yum -y update 
RUN yum -y groupinstall base

RUN yum -y install epel-release
RUN rpm -Uvh http://rpms.famillecollet.com/enterprise/remi-release-7.rpm

RUN yum -y install httpd httpd-devel
RUN rm -f /etc/httpd/conf.d/welcome.conf
RUN yum -y install --enablerepo=remi,remi-php70 php php-devel php-mbstring php-pdo php-gd php-pear
RUN yum -y install zip unzip

#RUN curl -sS https://getcomposer.org/installer | php -- --install-dir=/usr/local/bin --filename=composer
#RUN composer update
#RUN composer require twbs/bootstrap:4.3.1

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]

WORKDIR /var/www/html

