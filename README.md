# Introducció a Docker 2024

<!-- insert Docker logo here -->

![Docker logo](https://logos-marcas.com/wp-content/uploads/2021/03/Docker-Logo.png)

## Primera sessió

* Instal·lar Docker:
  * [Instal·ar WSL](https://docs.microsoft.com/en-us/windows/wsl/install)
  * [Instal·lar actualizació de Kernel de Linux](https://docs.microsoft.com/es-es/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)
  * [Instal·lar Docker Desktop en Windows](https://docs.docker.com/desktop/windows/install/)

* Hello World en Docker `docker run hello-world`

* Comandes bàsiques:
  * `docker ps`
  * `docker run`
  * `docker rm`
  * `docker logs`
  * `docker exec`
  * `docker stop`
  * `docker start`
  * `docker image`

* Eines i utilitats:
  * Visual Code: [Visual Code](https://code.visualstudio.com/):
    * Extensions a instal·lar:
      * Docker
      * Remote Development
      * SQL Server
      * MySQL
  * Azure Data Studio: [Azure Data Studio](https://azuredatastudio.net/)

## Segona sessió

* Persistència de les dades:
  * Muntatge carpetes locals
  * Volums:
    * Tipus de volums
    * Diferències entre `docker run --mount` i `docker run -v`

* Exemples entorns d'execució:
  * Usant SQL Server a un contenidor
  * Usant MySQL a un contenidor
  * Exemple codi Java amb remote development

* Arxiu Dockerfile
  * Creant imatge aplicació web
  * Bones pràctiques instal·lació durant creació
  * Etiquetat
  * Crear aplicació Java contenidor
  * Crear aplicació Java multistage

* Crear imatge a partir d'un contenidor
  * docker commit

* Treballant amb registres de contenidors
  * Docker Hub
  * Altres alternatives: Azure Container Registry
  * Etiquetes: `docker tag` versionatge i *latest*

## Tercera sessió

* Xarxes en docker
  * Tipus de xarxes
  * Exemples

* Docker-compose
  * Solució amb un sol contenidor
  * Desplegant solucions amb múltiples contenidors

* Empaquetant aplicacions amb Docker
  * Empaquetant aplicacions PHP

* Orquestració de contenidors
  * Docker Swarm
  * Kubernetes

* Desplegant contenidors al cloud
  * Azure
  * AWS

## Recursos i links interessants

* Tutorials i cursos
  * [Docker Docs](https://docs.docker.com)
  * [Learn Docker in a Month of Lunches](https://diamol.net)
  * [Docker Compose Tutorial: advanced Docker made simple](https://www.educative.io/blog/docker-compose-tutorial)
  * [Tutorial bàsic Docker Raspberri PI](https://blog.330ohms.com/2022/07/30/tutorial-basico-para-usar-docker-en-tu-raspberry-pi/)
* Curiositats
  * [WebAssembly: Docker without containers!](https://wasmlabs.dev/articles/docker-without-containers/)
  * [The Complete Guide to Docker Secrets](https://earthly.dev/blog/docker-secrets/)
  * [Introducción a Kubernetes para principiantes](https://geekflare.com/es/kubernetes-introduction/)
