# Ejemplo imagen multi-stage

## Descripción

En este caso vemos un ejemplo de cómo utilizar una imagen multi-stage para reducir el tamaño de la imagen final.

## Dockerfile
```dockerfile
FROM golang:1.18 as BUILDER
ADD go/ /go/example
RUN cd /go/example && go build .

FROM scratch
COPY --from=BUILDER /go/example/example /example

ENTRYPOINT [ "/example" ]
````
FROM golang:1.18: Utiliza la imagen base de Golang (Go) versión 1.18. 
    as BUILDER: Etiqueta esta etapa de construcción como BUILDER. Esto es útil en construcciones multi-stage para referirse a esta etapa posteriormente.

ADD go/ /go/example: Copia los contenidos del directorio go/ en el contexto de construcción del Dockerfile (es decir, el directorio desde donde se ejecuta docker build) al directorio /go/example dentro de la imagen. La instrucción ADD funciona de manera similar a COPY, pero puede manejar URL y archivos tar comprimidos además de copiar archivos y directorios.

RUN cd /go/example && go build .: Ejecuta dos comandos en la imagen:
    cd /go/example: Cambia el directorio de trabajo a /go/example.
    go build .: Compila el proyecto Go en el directorio actual (/go/example). El comando go build . construye un binario ejecutable del paquete principal (main) en ese directorio.

FROM scratch: Utiliza la imagen base scratch, que es una imagen vacía. Es la base más mínima posible y no contiene nada por defecto. Es útil para crear imágenes extremadamente ligeras.   

COPY --from=BUILDER /go/example/example /example:
    Copia el binario compilado example desde la etapa BUILDER (ubicado en /go/example/example) al directorio raíz (/) de la nueva imagen y lo renombra a /example.
    La opción --from=BUILDER indica que se debe copiar el archivo desde la etapa de construcción etiquetada como BUILDER.

ENTRYPOINT [ "/example" ]:
    Establece el comando que se ejecutará cuando se inicie el contenedor. En este caso, ejecutará el binario /example.    

Si miramos el tamaño de las imágenes, podemos ver cómo la imagen final es mucho más pequeña que la imagen de la fase de construcción.

# Para probarlo:
```bash
docker build -t demo-go .
docker run --rm demo-go
