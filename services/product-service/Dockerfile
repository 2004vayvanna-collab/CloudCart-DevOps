
# Stage 1: Build Spring Boot application
FROM eclipse-temurin:21-jdk-noble AS build

WORKDIR /app

COPY . .

RUN chmod +x mvnw && ./mvnw -B -DskipTests package

# Stage 2: Runtime image
FROM eclipse-temurin:21-jre-noble

# Apply available security updates
RUN apt-get -o Acquire::Retries=0 update \
    && apt-get -o Acquire::Retries=0 install -y \
       --only-upgrade apt libapt-pkg6.0t64 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /app

COPY --from=build /app/target/*.jar app.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app.jar"]
