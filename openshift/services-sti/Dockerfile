# springboot-gradle-centos7
FROM openshift/base-centos7

# LABEL maintainer="defcyy@gmail.com"

ENV BUILDER_VERSION 1.0

ENV GRADLE_VERSION 4.8

LABEL io.k8s.description="Platform for building springboot with gradle" \
     io.k8s.display-name="Springboot Gradle Builder" \
     io.openshift.expose-services="8080:http" \
     io.openshift.tags="builder,gradle-4.10.2,springboot"

# RUN yum install -y ... && yum clean all -y
RUN yum install -y curl unzip java-1.8.0-openjdk java-1.8.0-openjdk-devel && yum clean all -y && \
    curl -sL -0 https://services.gradle.org/distributions/gradle-${GRADLE_VERSION}-bin.zip -o /tmp/gradle-${GRADLE_VERSION}-bin.zip && \
    unzip /tmp/gradle-${GRADLE_VERSION}-bin.zip -d /usr/local/ && \
    rm /tmp/gradle-${GRADLE_VERSION}-bin.zip && \
    mv /usr/local/gradle-${GRADLE_VERSION} /usr/local/gradle && \
    ln -sf /usr/local/gradle/bin/gradle /usr/local/bin/gradle && \
    mkdir -p /opt/openshift && \
    mkdir -p /opt/app-root/source && chmod -R a+rwX /opt/app-root/source && \
    mkdir -p /opt/s2i/destination && chmod -R a+rwX /opt/s2i/destination && \
    mkdir -p /opt/app-root/src && chmod -R a+rwX /opt/app-root/src

ENV PATH=/opt/gradle/bin/:$PATH

# COPY ./<builder_folder>/ /opt/app-root/

# sets io.openshift.s2i.scripts-url label that way, or update that label
COPY s2i /usr/libexec/s2i

RUN chown -R 1001:1001 /opt/openshift

# This default user is created in the openshift/base-centos7 image
USER 1001

EXPOSE 8080

CMD ["/usr/libexec/s2i/usage"]
