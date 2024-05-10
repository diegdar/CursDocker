# Dockerfile multi entorn

## Descripció

Una situació habitual és necessitar un `Dockerfile` per la fase de desenvolupament i després un altre per la fase de producció.

Una primera aproximació pot ser tenir dos `Dockerfile` diferents, però això pot portar a problemes de manteniment, ja que si cal modificar alguna cosa, caldrà fer-ho en els dos fitxers.

Una altra opció és tenir un únic `Dockerfile` que sigui vàlid per a les dues fases. Això es pot aconseguir amb la instrucció `AS` i amb la instrucció `FROM` de forma similar a com hem vist en les solucions multi-stage.

## Dockerfile

```dockerfile
FROM php:8.1-apache as dev
# install mysql extension
RUN apt update && \
    docker-php-ext-install mysqli pdo pdo_mysql && \
    apt clean

FROM dev as prod
ADD /code/ /var/www/html/
```

## Construcció de la imatge

Amb el paràmetre `--target` podem indicar quina fase volem construir.

```bash
docker build -t multi-env . --target dev
```

Ens permetrà construir la imatge per a la fase de desenvolupament, que podrem usar per desenvolupar el codi amb un volum de tipus bind.

```bash
docker run -d -p 8080:80 --mount type=bind,target=/var/www/html,source=./ \ multi-env
```

Quan ja tenim el codi llest per a producció, podem construir la imatge per a la fase de producció.

```bash
docker build -t multi-env . --target prod
```

Podem comprovar com el codi ja està empaquetat dins de la imatge.

```bash
docker run -d -p 8080:80 multi-env
```
