FROM maven:3.8.6-openjdk-11 AS common-data-service-builder

WORKDIR /app

COPY common-data-service/pom.xml .

RUN mvn dependency:go-offline

COPY common-data-service/src ./src

RUN mvn package -DskipTests


FROM openjdk:11.0.16-jdk

WORKDIR /app

COPY --from=common-data-service-builder /app/target/*.jar app/test.jar

EXPOSE 8082

ENTRYPOINT ["java", "-jar", "app/test.jar"]