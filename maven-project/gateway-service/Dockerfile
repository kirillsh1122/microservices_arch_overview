FROM maven:4.0.0-rc-5-eclipse-temurin-21-alpine AS build
WORKDIR /app
COPY gateway-server/pom.xml gateway-server/pom.xml
RUN mvn -f gateway-server/pom.xml dependency:go-offline
COPY gateway-server/src gateway-server/src
RUN mvn -f gateway-server/pom.xml clean package -Dmaven.test.skip=true

FROM eclipse-temurin:21-jre-alpine-3.23
WORKDIR /gateway-server
COPY --from=build /app/gateway-server/target/*.jar gateway-server.jar
EXPOSE 8085
CMD ["java", "-jar", "gateway-server.jar"]