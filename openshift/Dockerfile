FROM openjdk:8-jdk-alpine

VOLUME /tmp

EXPOSE 8080

COPY app.jar /

CMD ["java", "-jar", "/app.jar", "--server.port=8080"]