FROM centos:centos7

ENV JAVA_VERSION 1.8.0
RUN yum update -y && yum install -y java-"${JAVA_VERSION}"-openjdk-devel && yum clean all
ENV JAVA_HOME /usr/lib/jvm/java
