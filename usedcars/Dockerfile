# Build stage: kompajliramo Java kod
FROM maven:3.9.9-eclipse-temurin-17-focal AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Production stage: pokrećemo JAR
FROM openjdk:17-jdk-alpine
ARG PORT=9000
ENV PORT=${PORT}
COPY --from=build /app/target/*.jar /app/app.jar
EXPOSE ${PORT}
CMD ["sh", "-c", "java -jar /app/app.jar --server.port=${PORT}"]
