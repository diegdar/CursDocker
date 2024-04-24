# Exemple imatge multi-stage

## Descripció

En aquest cas veiem un exemple de com fer servir una imatge multi-stage per a reduir la mida de la imatge final.

## Dockerfile

```dockerfile
FROM golang:1.18 as builder
ADD go/ /go/example
RUN cd /go/example && go build .

FROM scratch
COPY --from=builder /go/example/example /example

ENTRYPOINT [ "/example" ]
```

Si mirem la mida de les imatges, podem veure com la imatge final és molt més petita que la imatge de la fase de construcció.