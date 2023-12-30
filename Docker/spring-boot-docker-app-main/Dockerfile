FROM ubuntu:22.04
MAINTAINER "Swapnil"
RUN apt-get -y update && apt-get install -y openjdk-11-jdk

# pull maven image and run maven command to create target folder
FROM maven:3.6.3-jdk-11 AS MAVEN_BUILD
COPY pom.xml /build/
COPY src /build/src/
WORKDIR /build/
RUN mvn clean install -DskipTests -Dmaven.test.skip=true
COPY target/spring-boot-docker-app.jar  /usr/app/
WORKDIR /usr/app/
EXPOSE 8082
ENTRYPOINT ["java", "-jar", "spring-boot-docker-app.jar"]
