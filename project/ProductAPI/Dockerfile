#stage1: build artifact
FROM maven:3.8.5.-jdk-8-slim AS builder
COPY . /builder/
WORKDIR /builder/
RUN mvn clean package 

#stage2: install java and copy artifact to container location
FROM openjdk:8-jre-slim
COPY --from=builder /builder/target/*.jar /app/ 
EXPOSE 8080
#ENTRYPOINT ["java","-jar","/app.jar"]

# set heap size
ARG MEMORYMIN=-Xms64m
ARG MEMORYMAX=-Xmx2048m
ENV JAVA_MIN $MEMORYMIN
ENV JAVA_MAX $MEMORYMAX
CMD java -XX:+PrintFlagsFinal $JAVA_MIN $JAVA_MAX -jar /app/*.jar 
