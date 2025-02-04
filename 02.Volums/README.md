# TRABAJANDO CON VOLUMENES

## Crearemos un primer volumen:
docker volume create --name volum_1

## Conectaremos el volumen al contenedor:
docker run -it --rm -v volumen_1:/var/data --name ubuntu1 ubuntu

## Añadimos contenido a la carpeta /var/data:
<!-- Esto crea un archivo de tipo txt en esta ruta con la frase: "Hello World" -->
``` language=bash
echo "Hello World" >> /var/data/test.txt 
```

## Salimos y (se elimina el contenedor automaticamente por el comando --rm)
``` language=bash
exit
```

## Creamos un segundo contenedor:
docker run -it --rm -v volumen_1:/var/data --name ubuntu2 ubuntu

## Comprobamos que el contenido de la carpeta /var/data existe:
<!-- Imprime el texto del archivo test.txt: "Hello World" -->
``` language=bash
cat /var/data/test.txt
```

## Salimos y eliminamos el contenedor