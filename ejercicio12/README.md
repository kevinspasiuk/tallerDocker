# Taller Docker ej12

Resolución del ejercicio 12 de taller docker 2023

## Consigna

Escribir el descriptor yaml (deployment) para correr la aplicación PasswordAPI (https://hub.docker.com/r/nicopaez/password-api) en Kubernetes (okteto) con 3 replicas.

Agrega un service con auto-ingress

Una vez completo, compartir el link al repositorio (carpeta ejercicio12) con el correspondiente descriptor y las instrucciones que utilizaste y la URL pública para verlo funcionar.

## Resolución

Primero se creó el deployment:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: passwordapi
  labels:
    app: passwordapi
spec:
  replicas: 3
  selector:
    matchLabels:
      app: passwordapi
  template:
    metadata:
      labels:
        app: passwordapi
    spec:
      containers:
      - name: passwordapi
        image: nicopaez/password-api
```

Luego se creó el service según lo visto en clase, donde se mapea el puerto 3000 de la app al 8080:

```yaml
kind: Service
apiVersion: v1
metadata:
  name: passwordapi
  labels:
    app: passwordapi
  annotations:
    dev.okteto.com/auto-ingress: "true"
spec:
  selector:
    app: passwordapi
  ports:
  - protocol: TCP
    port: 8080
    targetPort: 3000
```

Okteto nos generó la siguiente url: https://passwordapi-kevinspasiuk.cloud.okteto.net/