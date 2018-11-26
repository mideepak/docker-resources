FROM centos:7

MAINTAINER This is Httpd image created by ITHelp-Stream <ithelp.stream@gmail.com>

RUN yum update all && yum -y install httpd && yum clean all

EXPOSE 80

VOLUME /opt/ /opt

ADD index.html /var/www/html

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]

