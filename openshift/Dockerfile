FROM openjdk:8-jdk-alpine

VOLUME /tmp

ENV APP_PORT 8080
ENV APP_ENV dev

EXPOSE $APP_PORT

COPY app.jar /

CMD ["sh", "-c", "java -jar /app.jar --server.port=$APP_PORT --spring.profiles.active=$APP_ENV"]