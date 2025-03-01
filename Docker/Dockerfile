FROM openjdk:17-jdk-alpine 

WORKDIR /app 

COPY src/app.java /app/app.java 

COPY mysql-connector-java-8.0.33.jar /app/mysql-connector-java.jar

RUN apt-get update && \
    apt-get install -y mysql-server && \
    apt-get clean

RUN javac src/app.java

CMD['java','app']

