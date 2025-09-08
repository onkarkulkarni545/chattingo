# Stage 1: Build with Maven
FROM maven:3.9.8-eclipse-temurin-20 AS builder
WORKDIR /build
COPY pom.xml .
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Production runtime
FROM eclipse-temurin:20-jre-jammy AS runner
WORKDIR /app
COPY --from=builder /build/target/*.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java","-jar","app.jar"]
