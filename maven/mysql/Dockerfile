FROM vaysman/buildpack:maven339-jdk8

ENV MYSQL_VERSION 5.6
RUN curl -s http://repo.mysql.com/mysql57-community-release-el7.rpm > mysql57-community-release-el7.rpm &&\
    rpm -ih mysql57-community-release-el7.rpm &&\
    rm mysql57-community-release-el7.rpm &&\
    yum update -y &&\
    yum-config-manager --disable mysql57-community &&\
    yum-config-manager --enable mysql56-community &&\
    yum install -y mysql-server &&\
    groupadd --gid 596 docker &&\
    usermod -a --groups docker jenkins &&\
    yum clean all
