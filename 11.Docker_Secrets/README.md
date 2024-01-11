# Docker Secrets

Un secret és qualsevol dada, com ara una contrasenya, un certificat o una clau API, que no s’ha de transmetre a través d’una xarxa ni emmagatzemar-les sense xifrar en un Dockerfile o en el codi font de la vostra aplicació.

Docker Compose us proporciona una manera d’utilitzar secrets sense haver d’utilitzar variables d’entorn per emmagatzemar informació. Si injecteu contrasenyes i claus API com a variables d’entorn, podeu arriscar una exposició involuntària a la informació. Les variables de medi ambient solen estar disponibles per a tots els processos i pot ser difícil fer un seguiment de l’accés. També es poden imprimir en registres quan es debutin errors sense el vostre coneixement. L’ús de secrets mitiga aquests riscos.

Veiem l'exemple:

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