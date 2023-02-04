#
# Build stage
#
FROM maven:3.6.0-jdk-11-slim AS build
COPY src /home/app/src
COPY pom.xml /home/app
RUN mvn -f /home/app/pom.xml clean package

#
# Package stage
#
FROM openjdk:11-jre-slim
COPY --from=build /home/app/target/*.jar /usr/local/lib/app.jar
RUN useradd -ms /bin/bash java-app && \
    chown -R java-app:java-app /usr/local/lib/app.jar
USER java-app
ENTRYPOINT ["java","-jar","/usr/local/lib/app.jar"]
