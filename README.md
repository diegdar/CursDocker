# Introducció a Docker

<!-- insert Docker logo here -->

![Docker logo](https://logos-marcas.com/wp-content/uploads/2021/03/Docker-Logo.png)

<!-- insert BCN Activa logo here -->

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

* Eines i utilitats:
  * Visual Code: [Visual Code](https://code.visualstudio.com/)
  * Azure Data Studio: [Azure Data Studio](https://azuredatastudio.net/)

## Segona sessió

* Persistència de les dades:
  * Muntatge carpetes locals
  * Volums

* Exemples entorns d'execució:
  * Usant SQL Server a un contenidor
  * Exemple codi Java

* Arxiu Dockerfile

* Treballant amb registres de contendidors
  * Docker Hub
  * Altres alternatives: Azure Container Registry

## Tercera sessió

* Xarxes en docker
  * Tipus de xarxes
  * Exemples

* Docker-compose
  * Solució amb un sol contenidor
  * Desplegant solucions amb múltiples contenidors

* Orquestració de contenidors
  * Docker Swarm
  * Kubernetes

* Desplegant contenidors al cloud
  * Azure
  * AWS
