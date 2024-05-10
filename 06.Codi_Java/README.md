# Contenedor aplicación consola Java

## Autobuild

Ejemplo de cómo dockerizar una aplicación sencilla de Java por consola

El programa Java es el clásico que se le pasa un entero como argumento y pinta un triángulo con * con el número de filas correspondiente al argumento.

```java
import java.io.*;
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
             System.out.println("Argumento must be an integer");
         }
     }
}
````

Descripción del Dockerfile

```Dockerfile
   FROM openjdk:latest
   COPY. /usr/src/myapp
   WORKDIR /usr/src/myapp
   RUN javac Main.java
   ENTRYPOINT [ "java","Main"]
   CMD ["5"]
````

> FROM: Usamos como imagen base la última de openjdk.
>
> COPY copiamos en el contenedor la carpeta donde toca toda la carpeta de trabajo.
>
> WORKDIR establecemos como directorio de trabajo para el resto de comandos la carpeta /usr/src/myapp.
>
> RUN aquí compilamos nuestro archivo java
>
> ENTRYPOINT sirve para ejecutar java y le pasamos como argumento el programa compilado
>
> CMD establecemos un argumento por defecto, por si no le pasamos ninguno, toma el valor 5

Para probarlo:

```bash
docker build -t demo-java .

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

También podemos pasarle un argumento específico:

````
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