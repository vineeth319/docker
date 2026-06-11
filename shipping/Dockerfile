# Build Stage
FROM maven:3.9.14 AS builder

WORKDIR /app

# Copy dependency definition first for better caching
COPY pom.xml .

# Copy source code
COPY src ./src

# Build application
RUN mvn clean package && \
    mv target/*.jar shipping.jar

# Runtime Stage
FROM eclipse-temurin:17-jre-alpine

WORKDIR /app

# Create non-root user
RUN addgroup -S roboshop && \
    adduser -S roboshop -G roboshop

# Copy artifact with correct ownership
COPY --from=builder --chown=roboshop:roboshop /app/shipping.jar .

EXPOSE 8080

USER roboshop

ENTRYPOINT ["java","-jar","shipping.jar"]