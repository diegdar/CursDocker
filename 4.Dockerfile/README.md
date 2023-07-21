# Creació imatge Docker

Tenim un arxiu Dockerfile que conté els comands necessaris per crear una imatge Docker que permetrà executar el conegut joc 2048.

```language-bash
docker build -t calonso6/2048 .
```

Provem el nostre contenidor:

```language-bash
docker run -it --rm --name 2048 calonso6/2048
```

Un cop creada la imatge es pot publicar al repositori DockerHub o al que vulguem:

```language-bash
docker push calonso6/2048
```
### Construir imatges multiplataforma ##

Provat amb la versió 3.5.2 de Docker Desktop i la versió 20.10.7 de Docker Engine.

Per configurar `buildx`:

```
$ docker buildx create --name mbuilder
$ docker buildx use mbuilder
% docker buildx inspect --bootstrap                                                                        
Name:   mbuilder
Driver: docker-container

Nodes:
Name:      mbuilder0
Endpoint:  unix:///var/run/docker.sock
Status:    running
Platforms: linux/arm64, linux/amd64, linux/riscv64, linux/ppc64le,
linux/s390x, linux/386, linux/mips64le, linux/mips64, linux/arm/v7,
linux/arm/v6
```

Abans de construir la imatge ens hem de llogar a Docker Hub, perquèla imatge multiplataforma no s'emmagatzema en local, sinó que cal pujar-la al repositori.

```
$ docker login -u calonso6
```

I ara ja podem crear una imatge capaç d'executar-se a la arquitectura `linux/amd64` i `linux/arm64`:

```
$ docker buildx build --platform linux/amd64,linux/arm64 -t calonso6/2048:latest --push .
```

Amb aquesta ordre es construeix la imatge multiplataforma i es puja a Docker Hub.

## Executar la imagen en local ##

Com sempre, per executar la imatge, farem `docker run`.
Docker examinarà l'arquitectura de l'ordinador i descarregarà la imatge apropiada.

```
$ docker run -dp 8000:80 caonso6/2048
```

Si estem en una màquina Intel baixarà la imatge `linux/amd64` i si estem en un MacBook M1 es baixarà la imatge `linux/arm64`.
