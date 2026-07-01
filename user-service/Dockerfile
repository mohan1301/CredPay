FROM maven:3.9-eclipse-temurin-21 AS build
WORKDIR /build
COPY pom.xml .
RUN mvn dependency:go-offline #Download dependencies
COPY src ./src
RUN mvn clean package -DskipTests #Build the application
RUN ls -l /build/target
FROM eclipse-temurin:21-jre-alpine
WORKDIR /app
COPY --from=build /build/target/user-service-0.0.1-SNAPSHOT.jar app.jar
USER appuser
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
