FROM maven:3.8.6-openjdk-11 AS authentication-service-builder

WORKDIR /app

COPY authentication-service/pom.xml .

RUN mvn dependency:go-offline

COPY authentication-service/src ./src

RUN mvn package -DskipTests


FROM openjdk:11.0.16-jdk

WORKDIR /app

COPY --from=authentication-service-builder /app/target/*.jar app/test.jar

EXPOSE 8080

ENTRYPOINT ["java", "-jar", "app/test.jar"]