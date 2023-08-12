# Taller Docker ej04

Resolución del ejercicio 06 de taller docker 2023

## Consigna

Crear un contenedor para la aplicación PasswordApi (del ejercicio 4) que esté basada en la imagen redhat-openjdk-18/openjdk18-openshift
disponible en la registry de Red Hat (https://catalog.redhat.com/software/containers/redhat-openjdk-18/openjdk18-openshift/58ada5701fbe981673cd6b10).


1. Escribe el dockerfile
2. Genera la imagen (docker build)
3. Publica la imagen en tu cuenta de Dockerhub


## Resolución

1. Se descargó el .jar en una carpeta /ejercicio04
2. Se creo el Dockerfile en la misma carpeta 

```Dockerfile
FROM registry.access.redhat.com/redhat-openjdk-18/openjdk18-openshift:1.15-7
COPY passwordapi.jar /app/passwordapi.jar
WORKDIR /app
CMD ["java", "-jar", "passwordapi.jar"]
```
3. Se buildeó la imagen

```bash
$ docker build -t kevinspasiuk/tallerdocker-ej06 .
```

4. Se corrió la imagen

```bash
$ docker run -p 4567:8080 kevinspasiuk/tallerdocker-ej04
```
![image info](./img/ejercicio04.PNG)

5.  Se subió la imagen a docker hub 

```bash
$ docker image push kevinspasiuk/tallerdocker-ej04:latest
```

https://hub.docker.com/repository/docker/kevinspasiuk/tallerdocker-ej04/general
