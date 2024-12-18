# Use OpenJDK as the base image
FROM openjdk:17-jdk-alpine

# Set the working directory inside the container
WORKDIR /app

# Copy the built JAR into the image
COPY target/*.jar app.jar

# Copy Maven Wrapper files and POM file
COPY .mvn/ .mvn
COPY mvnw pom.xml ./

# Ensure Maven Wrapper is executable
RUN dos2unix ./mvnw && chmod +x ./mvnw

# Download dependencies to prepare for offline mode
RUN ./mvnw dependency:go-offline

# Copy the application source code
COPY src ./src

# Build the application
RUN ./mvnw package

# Expose the application port
EXPOSE 8080

# Set the default command to run the application
CMD ["java", "-jar", "target/*.jar"]
