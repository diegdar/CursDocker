# Exemple de com modificar el compose en funció de l'entorn

Tenim un arxiu `docker-compose.yml` inicial:

```yaml
version: '3.9'
services:
  php:
    image: php:7.4-apache
    volumes:
      - ./code:/var/www/html
    ports:
      - 8080:80
```

Quan aixequem l'entorn amb `docker-compose up -d` ens crea un contenidor amb un servidor apache i php 7.4 que escolta al port 8080. Aquest entorn serà ideal per desenvolupar, ja que ens permet editar el codi en local i provar-ho sobre el contenidor.

Quan volem desplegar l'entorn en mode producció