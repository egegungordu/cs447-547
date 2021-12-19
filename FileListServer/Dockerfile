FROM alpine/git as clone
WORKDIR /app
RUN git clone https://github.com/egegungordu/cs447-547.git

FROM maven:3.5-jdk-8-alpine as build
WORKDIR /app
COPY --from=clone /app/cs447-547/FileListServer /app
RUN ["mvn", "compile"]
RUN ["mvn", "verify"]
RUN ["mvn", "package"]

FROM openjdk:8-jre-alpine
WORKDIR /app
COPY --from=build /app/target/FileListServer-1.0.0.jar /app
COPY --from=build /app/target/lib /app/lib
COPY --from=build /app/tc /app/tc
COPY --from=clone /app/cs447-547/FileListServer/files /app/files
RUN apk update && apk add bash iproute2
