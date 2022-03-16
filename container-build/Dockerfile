FROM registry.access.redhat.com/ubi8/ubi:8.0

LABEL Component="httpd" \ 
      Name="do288/httpd" \
      Version="1.0" \
      Release="1"

# Labels consumed by OpenShift
LABEL io.k8s.description="A basic Apache HTTP Server image" \
      io.k8s.display-name="Apache HTTP Server parent image" \
      io.openshift.expose-services="8080:http" \
      io.openshift.tags="apache, httpd"

MAINTAINER Oscar Ballesteros oballest@redhat.com

ENV DOCROOT=/var/www/html

RUN yum install -y --disableplugin=subscription-manager httpd && \
    yum clean all --disableplugin=subscription-manager -y && \
    rm -rf /run/httpd && mkdir /run/httpd

RUN sed -i "s/Listen 80/Listen 8080/g" /etc/httpd/conf/httpd.conf && \
    sed -i "s/#ServerName www.example.com:80/ServerName 0.0.0.0:8080/g" /etc/httpd/conf/httpd.conf && \
    echo "Hello from the httpd container!" > ${DOCROOT}/index.html && \
    chgrp -R 0 /var/log/httpd /var/run/httpd && \
    chmod -R g=u /var/log/httpd /var/run/httpd

EXPOSE 8080

USER root

CMD ["/usr/sbin/httpd","-D","FOREGROUND"]


