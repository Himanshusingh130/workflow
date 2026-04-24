# Build stage
FROM eclipse-temurin:21-jdk-jammy AS builder

WORKDIR /app
COPY pom.xml .
COPY App.java .
COPY Apptest.java .
COPY src ./src

RUN apt-get update && apt-get install -y maven && rm -rf /var/lib/apt/lists/* && \
    mvn clean package -DskipTests

# Runtime stage
FROM eclipse-temurin:21-jdk-jammy

WORKDIR /app
COPY --from=builder /app/target/*.jar app.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app.jar"]
