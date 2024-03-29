# Use a base image with Maven and JDK installed
FROM maven:3.8.4-openjdk-11 AS builder

# Set the working directory in the container
WORKDIR /app

# Copy the Maven project file and pom.xml
COPY pom.xml .

# Copy the source code
COPY src ./src

# Build the application
RUN mvn clean package -DskipTests

# Create a new image with just the JAR file
FROM openjdk:11-jre-slim

# Set the working directory in the container
WORKDIR /app

# Copy the JAR file from the previous stage
COPY --from=builder /app/target/ApiGateway-0.0.1-SNAPSHOT.jar .

# Expose the port
EXPOSE 8080

# Command to run the application
CMD ["java", "-jar", "ApiGateway-0.0.1-SNAPSHOT.jar"]
