#FROM is the base image for which we will run our application
FROM nginx:latest
# Copy files and directories from the application - si queremos copiar todo el contenido de una carpeta debe terminar con una barra (html/)

# hay que poner todas las acciones juntas seguidas de && para que si alguna falla no se ejecuten las demas
RUN apt update && apt install -y nano && apt clean
ADD html/ /usr/share/nginx/html

# Tell Docker we are going to use this port
EXPOSE 80