FROM bitnami/git:latest AS stage1
WORKDIR /repo
ARG REPO_URL=https://github.com/sushmitha2580/Ekart.git
RUN git clone $REPO_URL .
CMD ["bash"]

FROM maven:amazoncorretto AS stage2
WORKDIR /repo
COPY --from=stage1 /repo/src/ /repo/src/
COPY --from=stage1 /repo/pom.xml /repo/pom.xml
RUN mvn clean package -DskipTests=true
CMD ["bash"]

FROM openjdk:8u151-jdk-alpine3.7
EXPOSE 8070
ENV test /usr/src/app
COPY --from=stage2 /repo/target/shopping-cart-0.0.1-SNAPSHOT.jar $test/app.jar
WORKDIR $test
ENTRYPOINT exec java -jar app.jar

