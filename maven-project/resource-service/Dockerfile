FROM maven:4.0.0-rc-5-eclipse-temurin-21-alpine AS build
WORKDIR /resource-service
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package

FROM eclipse-temurin:21-jre-alpine-3.23
WORKDIR /resource-service
COPY --from=build /resource-service/target/*.jar resource-service.jar
EXPOSE 8080
CMD ["java", "-jar", "resource-service.jar"]