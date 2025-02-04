# Dockerfile multi entorno

## Descripción

Una situación habitual es necesitar un `Dockerfile` para la fase de desarrollo y después otro para la fase de producción.

Una primera aproximación puede ser tener dos `Dockerfile` diferentes, pero esto puede llevar a problemas de mantenimiento, ya que si es necesario modificar algo, habrá que hacerlo en ambos archivos.

Otra opción es tener un único `Dockerfile` que sea válido para ambas fases. Esto se puede conseguir con la instrucción `AS` y con la instrucción `FROM` de forma similar a como hemos visto en las soluciones multi-stage.

## Dockerfile

```dockerfile
FROM php:8.1-apache as dev
# install mysql extension
RUN apt update && \
     docker-php-ext-install mysqli pdo pdo_mysql && \
     apt clean

FROM dev as prod
ADD /code/ /var/www/html/
````

## Construcción de la imagen
Con el parámetro `--target` podemos indicar que fase queremos construir.
```bash
docker build -t multi-env . --target dev
````

Nos permitirá construir la imagen para la fase de desarrollo, que podremos utilizar para desarrollar el código con un volumen de tipo bind.
```bash
docker run -d -p 8080:80 --mount type=bind,target=/var/www/html,source=./ \ multi-env
````

Cuando ya tenemos el código listo para la producción, podemos construir la imagen para la fase de producción.
```bash
docker build -t multi-env . --target prod
````

Podemos comprobar cómo el código ya está empaquetado dentro de la imagen.
```bash
docker run -d -p 8080:80 multi-env
````