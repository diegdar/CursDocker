 FROM openjdk:latest
  COPY . /usr/src/myapp
  WORKDIR /usr/src/myapp
  RUN javac Main.java
  # el ENTRYPOINT ejecuta el programa
  ENTRYPOINT [ "java","Main"] 
  # este es el valor por defecto del parametro
  CMD ["5"] 