FROM composer/composer:1.1-php5

WORKDIR /

COPY composer.json /

RUN useradd -d /opt/jenkins -u 1000 jenkins &&\
    groupadd --gid 596 docker &&\
    usermod -a --groups docker jenkins

RUN composer -q install

ENV JAVA_VERSION 1.8.0
ENV JAVA_HOME /usr/lib/jvm/java
ARG MAVEN_VERSION=3.3.9
ARG USER_HOME_DIR="/root"
ENV MAVEN_HOME /usr/share/maven
ENV MAVEN_CONFIG "$USER_HOME_DIR/.m2"

RUN echo deb http://ftp.de.debian.org/debian jessie-backports main >> /etc/apt/sources.list
RUN echo "Acquire::http {No-Cache=True;};" > /etc/apt/apt.conf.d/no-cache

RUN DEBIAN_FRONTEND=noninteractive apt-get update &&\
    apt-get -yq install -t jessie-backports openjdk-8-jdk ca-certificates-java &&\
    mkdir -p /usr/share/maven /usr/share/maven/ref &&\
    curl -fsSL http://apache.osuosl.org/maven/maven-3/$MAVEN_VERSION/binaries/apache-maven-$MAVEN_VERSION-bin.tar.gz \
         | tar -xzC /usr/share/maven --strip-components=1 &&\
    ln -s /usr/share/maven/bin/mvn /usr/bin/mvn

run ln -s /usr/lib/jvm/java-8-openjdk-amd64 /usr/lib/jvm/java

COPY mvn-entrypoint.sh /usr/local/bin/mvn-entrypoint.sh
COPY settings-docker.xml /usr/share/maven/ref/

VOLUME "$USER_HOME_DIR/.m2"

ENTRYPOINT ["/usr/local/bin/mvn-entrypoint.sh"]
CMD ["mvn"]
