FROM centos:7

RUN yum update all && yum -y install httpd && yum clean all

EXPOSE 80

ADD index.html /var/www/html

ENTRYPOINT ["/usr/sbin/httpd", "-D", "FOREGROUND"]
