FROM centos:centos7

RUN useradd -d /opt/jenkins -u 1000 jenkins &&
    groupadd --gid 596 docker &&\
    usermod -a --groups docker jenkins

ENV JAVA_VERSION 1.8.0
RUN yum update -y && yum install -y java-"${JAVA_VERSION}"-openjdk-devel && yum clean all
ENV JAVA_HOME /usr/lib/jvm/java
