# Docker Compose amb un sol contenidor

Docker compose simplifica la creació de contenidors al permetre configurar de forma senzilla paràmetres i variables d'entorn.

Exemple amb SQL Server:

```docker-compose.yml
version: '3.9'

networks:
  app-network-public:
    driver: bridge

volumes:
  sql-data:
    
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
      - sql-data:/var/opt/mssql
      
```
