# Creación imagen Docker

Tenemos un archivo Dockerfile que contiene los comandos necesarios para crear una imagen Docker que permitirá ejecutar el conocido juego 2048.

# este comando construye una imagen de Docker llamada diegdar/2048 a partir de los archivos y scripts del directorio actual.
docker build -t diegdar/2048 .

# Probamos nuestros contenedor:
docker run -it --rm --name 2048 diegdar/2048

# Una vez creada la imagen se puede publicar en el repositorio DockerHub o en lo que queramos:
    ## indicamos que queremos iniciar sesion en docker e introducimos el usuario y contraseña(aunque no se visualice cuando escribimos la contraseña se estara recibiendo):
    docker login docker.io

    ##subimos la imagen a docker:
    docker push diegdar/2048

# También se puede indicar la *versión* añadiendo una etiqueta o *tag*:
docker tag diegdar/2048 diegdar/2048:v1.0

# Cerramos sesion en docker:
docker logout
