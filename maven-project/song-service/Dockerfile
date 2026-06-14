FROM maven:4.0.0-rc-5-eclipse-temurin-21-alpine AS build
WORKDIR /song-service
COPY pom.xml .
RUN mvn dependency:go-offline
COPY src ./src
RUN mvn clean package

FROM eclipse-temurin:21-jre-alpine-3.23
WORKDIR /song-service
COPY --from=build /song-service/target/*.jar song-service.jar
EXPOSE 8080
CMD ["java", "-jar", "song-service.jar"]