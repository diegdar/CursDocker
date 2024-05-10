# Contenedor mySQL

Otro ejemplo de contenedor es el de mySQL. En este caso, el contenedor se crea a partir de una imagen de mySQL que se encuentra en el repositorio de DockerHub. Esta imagen se descarga y ejecuta con el pedido:

```bash
docker volume create mysql-db-data
docker run --rm -d -p 3306:3306 --name mysql-db -e MYSQL_ROOT_PASSWORD=secret --mount src=mysql-db-data,dst=/var/lib/mysql mysql
````

El volumen mysql-db-data se crea para guardar los datos de la base de datos. Este volumen se monta en el contenedor de mySQL. Esto permite que los datos de la base de datos se mantengan aunque el contenedor se destruya.

Para conectarse a la base de datos puede utilizar herramientas como [MySQL WorkBench](https://www.mysql.com/products/workbench/) o extensiones de VSCode como [MySQL](https://marketplace.visualstudio.com /items?itemName=formulahendry.vscode-mysql).

Con la extensión MySQL da un error si intenta contactar con el usuario `root`. La solución es crear un usuario nuevo y conectarse con ese usuario. Para crear un usuario, será necesario en primer lugar, deberemos entrar en el contenedor de mySQL:

docker exec -it mysql_db bash

Una vez dentro del contenedor, crearemos un nuevo usuario:

```bash
**iniciamos el usuario en la linea de comandos de mysql:
mysql -u root -p

**Ahora nos pedira la contraseña que indicamos antes(aunque la escribamos no se mostrar en la consola pero si se esta haciendo!) : secret
````

```sql
CREATE USER 'user'@'%' IDENTIFIED WITH mysql_native_password BY 'secreto';
GRANT AJO PRIVILEGAS DONDE *.* TO 'user'@'%';
FLUSH PRIVILEGAS;
````

Y ahora cuando se crea la conexión usaremos el usuario `user` en lugar de `root`.