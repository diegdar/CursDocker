# Contenedor aplicación consola Java

## Autobuild
Ejemplo de cómo dockerizar una aplicación sencilla de Java por consola

El programa Java es el clásico que se le pasa un entero como argumento y pinta un triángulo con * con el número de filas correspondiente al argumento.

# Descripción del Dockerfile
```Dockerfile
   FROM openjdk:latest
   COPY. /usr/src/myapp
   WORKDIR /usr/src/myapp
   RUN javac Main.java
   ENTRYPOINT [ "java","Main"]
   CMD ["5"]
````

FROM usamos como imagen base la opción de openjdk.

COPY copiamos en el contenedor la carpeta donde toca toda la carpeta de trabajo.

WORKDIR establecemos como directorio de trabajo para el resto de comandos la carpeta /usr/src/myapp.

RUN aquí compilamos nuestro archivo java

ENTRYPOINT sirve para ejecutar java y le pasamos como argumento el programa compilado

CMD establecemos un argumento por defecto, por si no le pasamos ninguno, toma el valor 5

Para probarlo:

````
# Crear la imagen apartir del dockerfile:
docker build -t demo-java .

# Crea el contenedor y lo ejecuta apartir de la imagen creada:
docker run --rm demo-java

Con esto obtenemos el siguiente resultado:

*
**
***
****
*****
******
*******
********
*********
**********

También podemos pasarle un argumento específico:

````
docker run --rm demo-java 8
````

*
**
***
****
*****
******
*******
********
*********
**********