
# Stage 1: Build Spring Boot
FROM eclipse-temurin:21-jdk-noble AS build

WORKDIR /app

COPY . .

RUN chmod +x mvnw && ./mvnw -B -DskipTests package

# Stage 2: Run Spring Boot
FROM eclipse-temurin:21-jre-noble

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
