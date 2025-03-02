FROM openjdk:17-jdk-alpine 

WORKDIR /app 

COPY . .

#COPY mysql-connector-j-9.2.0.jar /app/mysql-connector-java.jar

RUN apt-get update && \
    apt-get install -y mysql-server && \
    apt-get clean

RUN javac src/App.java

CMD ["java","app"]

