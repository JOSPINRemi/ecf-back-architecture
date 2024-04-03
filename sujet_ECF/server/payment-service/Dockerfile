FROM maven:3.8.6-openjdk-11 AS payment-service-builder

WORKDIR /app

COPY payment-service/pom.xml .

RUN mvn dependency:go-offline

COPY payment-service/src ./src

RUN mvn package -DskipTests


FROM openjdk:11.0.16-jdk

WORKDIR /app

COPY --from=payment-service-builder /app/target/*.jar app/test.jar

EXPOSE 8081

ENTRYPOINT ["java", "-jar", "app/test.jar"]