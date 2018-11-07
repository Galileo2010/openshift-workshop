FROM openshift/jenkins-slave-base-centos7

ENV GRADLE_VERSION 4.8
RUN yum install -y curl unzip java-1.8.0-openjdk java-1.8.0-openjdk-devel && yum clean all -y && \
    curl -sL -0 https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o /tmp/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip /tmp/gradle-${GRADLE_VERSION}-bin.zip -d /usr/local/ && \
    rm /tmp/gradle-${GRADLE_VERSION}-bin.zip && \
    mv /usr/local/gradle-${GRADLE_VERSION} /usr/local/gradle && \
    ln -sf /usr/local/gradle/bin/gradle /usr/local/bin/gradle

ENV PATH=/opt/gradle/bin/:$PATH
