# Ejemplo imagen multi-stage

## Descripción

En este caso vemos un ejemplo de cómo utilizar una imagen multi-stage para reducir el tamaño de la imagen final.

## Dockerfile

```dockerfile
FROM golang:1.18 as builder
ADD go/ /go/example
RUN cd /go/example && go build .

FROM scratch
COPY --from=builder /go/example/example /example

ENTRYPOINT [ "/example" ]
````

Si miramos el tamaño de las imágenes, podemos ver cómo la imagen final es mucho más pequeña que la imagen de la fase de construcción.

# Para probarlo:
```bash
docker build -t demo-go .
docker run --rm demo-go
