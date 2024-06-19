# Contenedor aplicación consola Java multistage

Ejemplo de cómo dockerizar una aplicación sencilla de Java por consola

El programa Java es el clásico que se le pasa un entero como argumento y pinta un triángulo con * con el número de filas correspondiente al argumento.

```java
importe java.io.*;
public class Main
{

     // Function to print n files of stars
     public static void printStars(int n)
     {
         int y, j;
  
         // loop to handle number of rows
         for(i=0; i<n; i++)
         {
  
             // loop to handle number of columns
             //
             for(j=0; j<=i; j++)
             {
                 // printing stars
                 System.out.print("* ");
             }
  
             // end line
             System.out.println();
         }
    }
 
     public static void main(String[] args)
     {
         try
         {
             int n = Integer.parseInt(args[0].trim());
             printStars(n);
         }
         catch(NumberFormatException error)
         {
             System.out.println("Argument must be an integer");
         }
     }
}
````

Descripción del Dockerfile

```Dockerfile
FROM openjdk:latest AS BUILDER
COPY. /usr/src/myapp
WORKDIR /usr/src/myapp
RUN javac Main.java

FROM openjdk:latest
RUN mkdir /code
WORKDIR /code
COPY --from=BUILDER /usr/src/myapp/Main.class .
VOLUME /code
ENTRYPOINT [ "java","Main"]
CMD ["5"]
````

FROM openjdk:latest AS BUILDER: Esta línea define una etapa de construcción utilizando la imagen openjdk:latest y la etiqueta como BUILDER. La etiqueta BUILDER es un alias que se puede usar posteriormente en el Dockerfile para referirse a esta etapa específica.

> COPY copiamos en la carpeta del contenedor toda la carpeta de trabajo. Copia todo el contenido del contexto de construcción (el directorio actual desde donde se está ejecutando el comando docker build) al directorio /usr/src/myapp dentro de la imagen. Aquí es donde se copia el código fuente
>
> WORKDIR establecemos como directorio de trabajo para el resto de comandos la carpeta /usr/src/myapp. Cualquier comando subsiguiente se ejecutará en este directorio.
>
> RUN aquí compilamos nuestro archivo java. Compila el archivo Main.java usando javac, el compilador de Java. Esto generará el archivo Main.class en el mismo directorio.

// Imagen Final
FROM openjdk: latest. Define la imagen base final, nuevamente usando la última versión de OpenJDK.

RUN mkdir /code: Crea un directorio /code dentro de la nueva imagen.

WORKDIR code: Establece el directorio de trabajo a /code.

COPY --from=BUILDER /usr/src/myapp/Main.class .: Copia el archivo Main.class desde la etapa etiquetada como BUILDER (definida anteriormente) al directorio /code en esta nueva imagen. La opción --from=BUILDER indica que el archivo debe ser copiado desde la etapa de construcción BUILDER.

VOLUME code. Esta línea declara que el directorio /code es un volumen. Un volumen en Docker es un mecanismo para persistir datos generados. Los volúmenes son gestionados por Docker y se almacenan fuera del sistema de archivos del contenedor. Al declarar un volumen, Docker asegura que los datos en ese directorio persisten y pueden ser compartidos con otros contenedores.

ENTRYPOINT [ "java","Main"]: Establece el comando y sus argumentos que se ejecutarán cuando el contenedor arranque. En este caso, ejecutará java Main, que inicia el programa Java compilado.

CMD ["5"]: Proporciona un valor por defecto para el argumento que Main tomará. Este valor puede ser sobrescrito al iniciar el contenedor. En este caso, el programa Main recibirá 5 como argumento por defecto.

```bash
docker build -t demo-java .
docker run --rm demo-java
````

Con esto obtenemos el siguiente resultado:

> \*
>
> \* \*
>
> \* \* \*
>
> \* \* \* \*
>
> \* \* \* \* \*

También le podemos pasar un argumento específico:

```bash
docker run --rm demo-java 8
````

> \*
>
>\* \*
>
> \* \* \*
>
> \* \* \* \*
>
> \* \* \* \* \*
>
> \* \* \* \* \* \*
>
> \* \* \* \* \* \* \*
>
> \* \* \* \* \* \* \* \*