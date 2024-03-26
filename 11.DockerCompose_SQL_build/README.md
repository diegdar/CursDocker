# Docker Compose amb un sol contenidor

En aquest exemple, es crea un servei a partir d'una imatge personalitzada (Dockerfile) per solucionar el problema dels permisos a les carpetes de SQL Server.

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
    build:
      dockerfile: ./Dockerfile
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
