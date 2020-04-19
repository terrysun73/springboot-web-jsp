# springboot-web-jsp
springboot-web-jsp


Docker file
FROM alpine/git as clone
WORKDIR /app
RUN git clone https://github.com/terrysun73/springboot-web-jsp.git


FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY --from=clone /app/springboot-web-jsp /app
RUN mvn clean package


FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=build /app/target/hello-springboot-1.3.5.RELEASE.war /app
EXPOSE 8080
ENTRYPOINT ["sh", "-c"]
CMD ["java -jar hello-springboot-1.3.5.RELEASE.war"]

Access point: http://localhost:8080/
