# Exemple compose amb un sol servei

Desplegarem un servei Nginx en mode desenvolupament, que mapeja la carpeta web a dins el contenidor.

```yaml
version: "3.9"
services:
  webserver:
    image: nginx
    ports:
      - "8080:80"
    # - "80" Publica el port 80 a un port aleatori del host  
    volumes:
      - type: bind
        source: ./web
        target: /usr/share/nginx/html
        read_only: true
```

Si obrim un shell dins el contenidor, veurem que no podem modificar els fitxers de la carpeta web, perquè s'ha muntat en model de només lectura.

Per desplegar el servei, executem:

```bash
docker-compose -f compose-dev.yaml up -d
```

Per aturar el servei, executem:

```bash
docker-compose -f compose-dev.yaml down
```

L'arxiu `compose-prod.yaml` ens permet desplegar el mateix servei en mode producció, sense mapejar cap carpeta, copiant el contingut web a dins la imatge

```yaml
version: "3.9"
services:
  webserver:
    build: .
    image: calonso6/web-basic
    ports:
      - "8080:80"
    volumes:
  ```

Per desplegar el servei en mode producció, executem:

```bash
docker-compose -f compose-prod.yaml up -d
```

Si aturem el servei, modifiquem l'arxiu index.html i tornem a engegar el servei, veurem que no s'ha modificat l'arxiu index.html, perquè no s'ha tornat a construir la imatge.

Si volem assegurar que cada cop que despleguem el servei, es construeixi la imatge, executem:

```bash
docker-compose -f compose-prod.yaml up -d --build
```

Podem comprovar, com es crea una imatge amb el nom seleccionat, enlloc del nom per defecte.
