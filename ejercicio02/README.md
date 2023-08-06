# Taller Docker ej02

Resolución del ejercicio 02 de taller docker 2023

## Consigna

1. Descarga la imagen nicopaez/pingapp:3.0.0
2. Crear un repositorio en dockerhub
3. Sube la imagen descargada al repositorio creado
4. Crea una carpeta "ejercicio02" en tu repositorio y pon dentro de la misma un archivo README.md con el detalle de instrucciones que utilizaste para completar la tarea. 
5. Asegurate que la imagen queda publicada como pública.
6. Incluye al final de las instrucciones la sentencia docker pull exacta para descargar tu imagen.

## Resolución

Descarga de la imagen
```bash
$ docker image pull nicopaez/pingapp:3.0.0

$ docker image ls
REPOSITORY         TAG       IMAGE ID       CREATED       SIZE
nginx              latest    89da1fb6dcb9   9 days ago    187MB
nicopaez/pingapp   3.0.0     5021b0410677   2 years ago   883MB
```

Repositorio creado: 

kevinspasiuk/tallerdocker-ejercicio02: 
https://hub.docker.com/repository/docker/kevinspasiuk/tallerdocker-ejercicio02/general

Para subir la imagen:
1. Tagear la imagen
```bash
$ docker image tag nicopaez/pingapp:3.0.0 kevinspasiuk/tallerdocker-ejercicio02:v1
```
2. Login en la registry 
```bash
$ docker login 
```
3. Subir la imagen
```bash
$ docker image push kevinspasiuk/tallerdocker-ejercicio02:v1
```
Descarga de la imagen subida
```bash
$ docker image pull kevinspasiuk/tallerdocker-ejercicio02:v1
```