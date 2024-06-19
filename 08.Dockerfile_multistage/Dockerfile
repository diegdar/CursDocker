# Imagen base
FROM openjdk:latest AS BUILDER
# Copiamos el codigo fuente
COPY . /usr/src/myapp
# Establecemos el directorio de trabajo
WORKDIR /usr/src/myapp
# Compilamos
RUN javac Main.java

# Imagen final
FROM openjdk:latest 
# Crea un directorio /code dentro de la nueva imagen.
RUN mkdir /code
# Establecemos el directorio de trabajo
WORKDIR /code
# Copiamos el fichero compilado
COPY --from=BUILDER /usr/src/myapp/Main.class .

VOLUME /code
# Ejecuta java y pasamos como argumento el programa compilado
ENTRYPOINT [ "java","Main"]
# Ejecucion con valor por defecto
CMD ["5"]
