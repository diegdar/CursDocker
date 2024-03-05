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

També es pot indicar la *versió* afegint una etiqueta o *tag*:

```language-bash
docker tag calonso6/2048 calonso6/2048:v1.0
```
