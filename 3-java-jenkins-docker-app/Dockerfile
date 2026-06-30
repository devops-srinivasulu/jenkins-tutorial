FROM maven:3.9.4-eclipse-temurin-17 AS build
WORKDIR /app
COPY pom.xml ./
RUN mvn dependency:go-offline -B
COPY src ./src
RUN mvn clean package -DskipTests

# Stage 2: Run the Java app using Eclipse Temurin 17 JRE
FROM eclipse-temurin:17-jre
WORKDIR /app
COPY --from=build /app/target/java-jenkins-docker-1.0-SNAPSHOT.jar app.jar
EXPOSE 8080
CMD ["java", "-jar", "app.jar"]
