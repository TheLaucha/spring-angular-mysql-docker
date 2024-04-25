
# FROM registry.access.redhat.com/ubi8/openjdk-17 AS builder
FROM maven:3-openjdk-17 AS builder

# Build dependency offline to streamline build
WORKDIR /project
COPY pom.xml .
RUN mvn dependency:go-offline

COPY src src
RUN mvn package -Dmaven.test.skip=true

# WORKDIR /app

FROM openjdk:17-alpine

# COPY target/emp_backend-0.0.1-SNAPSHOT.jar /app.jar
COPY --from=builder /project/target/*.jar /app.jar

EXPOSE 8080

ENTRYPOINT ["java","-jar","app.jar"]