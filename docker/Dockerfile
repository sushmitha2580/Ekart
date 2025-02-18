FROM bitnami/git:latest AS stage1
WORKDIR /Ekart
ARG REPO_URL=https://github.com/sushmitha2580/Ekart.git
RUN git clone $REPO_URL /Ekart
COPY /Ekart /repo
CMD ["bash"]

FROM maven AS stage2
WORKDIR /build
COPY --from=stage1 /repo/src/ /build/src/
COPY --from=stage1 /repo/pom.xml /build/pom.xml
RUN mvn clean package

FROM openjdk:8u151-jdk-alpine3.7
EXPOSE 8070
ENV app /usr/src/app
COPY --from=stage2 /build/target/shopping-cart-0.0.1-SNAPSHOT.jar $app/app.jar
WORKDIR $app
ENTRYPOINT exec java -jar app.jar

