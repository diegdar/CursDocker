# Docker Secrets

Un secret és qualsevol dada, com ara una contrasenya, un certificat o una clau API, que no s’ha de transmetre a través d’una xarxa ni emmagatzemar-les sense xifrar en un Dockerfile o en el codi font de la vostra aplicació.

Els serveis només poden accedir als secrets quan, explícitament, se'ls ha concedit mitjançant un atribut de secrets dins de l'element de nivell superior dels serveis.

La declaració dels secrets defineix o fa referència a dades sensibles que es concedeixen als serveis de la vostra aplicació Compose. L'origen del secret és un fitxer o un entorn.

- file: el secret crea dins un arxiu a la ruta especificada.
- environment: el secret es gestiona com un valor d'una variable d'entorn.
- external: si es marca com true, external indica que el secret ja existeix, i per tant, Compose no mira de crear-lo. Si el secret no existeix, es produirà un error.
- name: el nom de l'objecte secret a Docker. Aquest camp s'utilitza per referenciar secrets que contenen caràcters especials.

Alguns exemples bàsics de com utilitzar els secrets de Docker són els següents:

```docker-compose.yml
secrets:
  server-certificate:
    file: ./server.cert
```

El secret `server-certificate` secret es crea com  <project_name>_server-certificate quan l'aplicació es desplegada, agafant el contingut del fitxer `server.cert` com un secret.

```docker-compose.yml
secrets:
  token:
    environment: "OAUTH_TOKEN"
```

En aquest segon exemple, el secret `token` es crea com  <project_name>_token quan l'aplicació es desplegada, agafant el valor de la variable d'entorn `OAUTH_TOKEN` com un secret.

El cas del repositori és el següent:

```docker-compose.yml
services:
   db:
     image: mysql:latest
     volumes:
       - db_data:/var/lib/mysql
     environment:
       MYSQL_ROOT_PASSWORD_FILE: /run/secrets/db_root_password
       MYSQL_DATABASE: wordpress
       MYSQL_USER: wordpress
       MYSQL_PASSWORD_FILE: /run/secrets/db_password
     secrets:
       - db_root_password
       - db_password

   wordpress:
     depends_on:
       - db
     image: wordpress:latest
     ports:
       - "8000:80"
     environment:
       WORDPRESS_DB_HOST: db:3306
       WORDPRESS_DB_USER: wordpress
       WORDPRESS_DB_PASSWORD_FILE: /run/secrets/db_password
     secrets:
       - db_password


secrets:
   db_password:
     file: db_password.txt
   db_root_password:
     file: db_root_password.txt

volumes:
    db_data:
```

- La línia de secrets de cada servei defineix els secrets de Docker que voleu injectar al contenidor específic.
- El segment de secrets principals defineix les variables `db_password` i `db_root_password` i un fitxer que s’ha d’utilitzar per definir els seus valors.
- El desplegament de cada contenidor significa que Docker crea un conjunt de fitxers temporals sota /run/secrets /<secret_name> amb els seus valors específics.

A diferència dels altres mètodes, això garanteix que els secrets només estan disponibles per als serveis que han estat explícitament atorgats a l'accés i que els secrets només existeixen en memòria mentre aquest servei funciona.

Prèviament hem creat els dos arxius de text amb les contrasenyes que volem utilitzar per a la base de dades.

```bash
echo "supersecret" > db_password.txt
echo "supersecret" > db_root_password.txt
```

Ara només cal executar:

```bash
docker-compose up -d
```

La gestió de secrets inicialment es va introduir a Docker Swarm, però ara també està disponible a Docker i Docker Compose tot i que amb algunes limitacions.

Podeu trobar informació sobre els secrets a la documentació oficial de Docker i d'altres publicacions:

- [How to use secrets in Docker Compose](https://docs.docker.com/compose/use-secrets/)
- [Docker Secrets : Beginners Guide](https://medium.com/@younusraza909/docker-secrets-beginners-guide-73f0b60764aa)
- [Docker Secrets Management](https://www.docker.com/blog/docker-secrets-management/)
