# Ejemplo compose con un solo servicio
Desplegaremos un servicio Nginx en modo desarrollo, que mapea la carpeta web dentro del contenedor.

```yaml
versión: "3.9"
servicios:
   webserver:
     image: nginx
     puertos:
       - "8080:80"
     # - "80" Publica el puerto 80 en un puerto aleatorio del host
     volúmenes:
       - type: bind
         source: ./web
         target: /usr/share/nginx/html
         read_only: true
````

Si abrimos un shell dentro del contenedor, veremos que no podemos modificar los archivos de la carpeta web, porque se ha montado en modelo de sólo lectura.

Para desplegar el servicio, ejecutamos:

```bash
docker-compose -f compose-dev.yaml up -d
````

Para detener el servicio, ejecutamos:

```bash
docker-compose -f compose-dev.yaml down
````

El archivo `compose-prod.yaml` nos permite desplegar el mismo servicio en modo producción, sin mapear ninguna carpeta, copiando el contenido web dentro de la imagen

```yaml
versión: "3.9"
servicios:
   webserver:
     build: .
     image: calonso6/web-basic
     puertos:
       - "8080:80"
     volúmenes:
   ````

Para desplegar el servicio en modo producción, ejecutamos:

```bash
docker-compose -f compose-prod.yaml up -d
````

Si detenemos el servicio, modificamos el archivo index.html y volvemos a poner en marcha el servicio, veremos que no se ha modificado el archivo index.html, porque no se ha vuelto a construir la imagen.

Si queremos asegurar que cada vez que desplegamos el servicio, se construya la imagen, ejecute:

```bash
docker-compose -f compose-prod.yaml up -d --build
````

Podemos comprobar, cómo se crea una imagen con el nombre seleccionado, en lugar del nombre por defecto.