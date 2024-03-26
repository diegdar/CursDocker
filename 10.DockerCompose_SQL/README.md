# Docker Compose amb un sol contenidor

Docker compose simplifica la creació de contenidors al permetre configurar de forma senzilla paràmetres i variables d'entorn.

Exemple amb SQL Server:

```yaml
version: '3.9'

networks:
  app-network-public:
    driver: bridge

volumes:
  sqlvolume:
  sqldata:
  sqllog:
  sqlbackup:
services:
  db:
    image: mcr.microsoft.com/mssql/server
    container_name: db-sqlserver
    networks:
      - app-network-public
    restart: always
    env_file:
      - sqlserver.env
      - sapassword.env
    ports:
      - '1433:1433'
    volumes:
      - sqlvolume:/var/opt/mssql/
      - sqldata:/var/opt/sqlserver/data
      - sqllog:/var/opt/sqlserver/log
      - sqlbackup:/var/opt/sqlserver/backup
      
```

Tenim l'arxiu `CreateDB.sql` que conté les instruccions per crear la base de dades `Music`.

```sql
CREATE DATABASE Music;
GO
```

Quan s'executa l'entorn i provem de llençar la consulta `CreateDB.sql` obtenim un error de `permission denied`. Si obrim un shell, podem observar com el contenidor s'està executant com un usuari `mssql` amb un `uid` i `gid` concrets, mentre que les carpetes corresponents als volums estan configurades per accés exclusiu de l'usuari `root`.

Per solucionar aquest problema (no és la millor solució des del punt de vista de seguretat), podem forçar que el contenidor s'executi com `root`, afegint a l'arxiu `docker-compose.yml` la següent línia:

```yaml
services:
  db:
    image: mcr.microsoft.com/mssql/server
    container_name: db-sqlserver
    user: root
    ...
```
