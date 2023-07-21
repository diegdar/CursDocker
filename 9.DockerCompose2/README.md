# Docker compose per orquestrar contenidors

Amb docker compose podem orquestrar contenidors de diferents tipus.

```docker-compose.yml
version: "3.9" 
services:
  web:
    build: .
    ports:
      - "8000:5000"
    volumes:
      - .:/code
      - logvolume01:/var/log
    links:
      - redis
  redis:
    image: redis
volumes:
  logvolume01: {}
```
