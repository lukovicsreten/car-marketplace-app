# Build stage - kompajliramo Java kod
FROM maven:3.8.6-openjdk-17-slim AS build
WORKDIR /app
COPY . .
RUN mvn clean package -DskipTests

# Production stage - pokrećemo JAR
FROM openjdk:17-slim
ARG PORT=9000
ENV PORT=${PORT}
COPY --from=build /app/target/*.jar /app/app.jar
EXPOSE ${PORT}
CMD ["sh", "-c", "java -jar /app/app.jar --server.port=${PORT}"]