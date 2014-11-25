# Base Ubuntu Precise 12.04 LTS image
#
FROM ubuntu:14.04
MAINTAINER fonhorst alipoov.nb@gmail.com

# Setup a volume for data
VOLUME ["/data"]

# Very bad thing. Some workaround should be invented.
ENV http_proxy http://proxy.ifmo.ru:3128
ENV https_proxy http://proxy.ifmo.ru:3128

# Set correct source list
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty main universe" > /etc/apt/sources.list
RUN echo "deb http://archive.ubuntu.com/ubuntu trusty-updates main universe" >> /etc/apt/sources.list

RUN  /etc/resolv.conf && echo 'nameserver 127.0.1.1' > /etc/resolv.conf

RUN cat /etc/resolv.conf
RUN cat /etc/hosts

# install a few other useful packages plus Open Jdk 7
RUN apt-get update && apt-get upgrade -y && apt-get install -y less openjdk-7-jre-headless net-tools vim-tiny sudo openssh-server iputils-ping python2.7

# Install Hadoop
ADD http://apache-mirror.rbc.ru/pub/apache/spark/spark-1.1.0/spark-1.1.0-bin-hadoop2.4.tgz /opt/
RUN tar xzvf /opt/spark-1.1.0-bin-hadoop2.4.tgz /opt/spark-1.1.0


# Docker messes up /etc/hosts and adds two entries for 127.0.0.1
# we try to recover from that by giving /etc/resolv.conf and therefore
# the nameserver priority
RUN sed -i s/"files dns"/"dns files"/ /etc/nsswitch.conf

# add config file templates
ADD files /root/spark_files

# Set JAVA_HOME
ENV JAVA_HOME /usr/lib/jvm/java-7-openjdk-amd64
