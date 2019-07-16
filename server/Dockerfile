#Very similar to the springboot hello world Dockerfile

#try to use a multi stage file

FROM maven:latest as base
WORKDIR /build
COPY . .
RUN mvn clean package
FROM java:8
WORKDIR /opt/app
COPY --from=base /build/target/Spring_Day_Two-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["/usr/bin/java", "-jar", "app.jar"]


