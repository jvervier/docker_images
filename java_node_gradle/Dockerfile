#If used from Jenkins, you should run the image with -u root args

LABEL creator="Jérôme Vervier"

FROM ubuntu:16.04

ENV JAVA_VERSION_MAJOR=8 \
    JAVA_VERSION_MINOR=161 \
    JAVA_VERSION_BUILD=12 \
    JAVA_PACKAGE=jdk \
    JAVA_HOME=/usr \
    GRADLE_VERSION=4.6 \
    GRADLE_HOME=/opt/gradle

ENV PATH=$PATH:${JAVA_HOME}/bin:${GRADLE_HOME}:${GRADLE_HOME}/bin

# install required packages
RUN apt-get update -qq && apt-get -y -qq --no-install-recommends install locales git unzip bash curl wget ca-certificates libapparmor1

# set locales
RUN echo "en_US.UTF-8 UTF-8" >> /etc/locale.gen && \
    locale-gen en_US.utf8 && \
    /usr/sbin/update-locale LANG=en_US.UTF-8
ENV LANG=en_US.UTF-8 LC_ALL=en_US.UTF-8

# install java
RUN apt-get -y install openjdk-8-jdk

# install gradle
RUN mkdir -p /tmp/gradle ${GRADLE_HOME} && cd /tmp/gradle && \
    wget -qO- -O gradle.zip https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip -qq gradle.zip && \
    mv ./gradle-${GRADLE_VERSION}/* ${GRADLE_HOME}/

RUN apt-get -y install python-software-properties

RUN curl -sL https://deb.nodesource.com/setup_8.x -o nodesource_setup.sh
RUN bash nodesource_setup.sh

RUN apt-get -y install nodejs

RUN apt-get -y install build-essential

RUN npm -g config set user root

RUN npm install --quiet --no-progress -g @angular/cli
RUN npm cache clean --force

# cleanup
RUN rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* ${JAVA_HOME}/*src.zip && apt-get clean