FROM openjdk:latest AS BUILDER
COPY . /usr/src/myapp
WORKDIR /usr/src/myapp
RUN javac Main.java

FROM openjdk:latest 
RUN mkdir /code
WORKDIR /code
COPY --from=BUILDER /usr/src/myapp/Main.class .
VOLUME /code
ENTRYPOINT [ "java","Main"]
CMD ["10"]
