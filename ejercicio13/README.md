# Taller Docker ej13

Resolución del ejercicio 13 de taller docker 2023

## Consigna

Escribir todos los descriptores faltantes necesarios para correr en kubernetes la aplicación jobvacancy considerando:

* El descriptor adjunto
* La aplicación requiere de 2 variables: RACK_ENV: "production" y PORT: "3000"
* La aplicación espera una variable DATABASE_URL con url de conexión a la base de datos postgres

IMPORTANTE: hay que desplegar un contenedor postgresql (postgres:10.4) no un cluster de postgresql y no se preocupen por utilizar un volumen persistente. Levanten el contenedor y que guarde datos locales, es solo para jugar.

Ubica los descriptores en una carpeta ejercicio13 en tu repositorio personal y entrega el link.

## Resolución

Primero se crearon las env variables para el container jobvacancy en configmap-env.yaml:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: jobvacancyconfig
  labels:
    app: jobvacancy
data:
  RACK_ENV: "production"
  PORT: "3000"
```

Después se creó el secret para la conexión a la base de datos, se encodeó en base64 el siguiente string: postgres://postgres:Passw0rd!@localhost:5432/postgres. Reemplacé @db por @localhost para que funcione.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: jobvacancysecret
type: Opaque
data:
  DATABASE_URL: cG9zdGdyZXM6Ly9wb3N0Z3JlczpQYXNzdzByZCFAbG9jYWxob3N0OjU0MzIvcG9zdGdyZXM=
```

Por último se agrego el container de postgres y se usó otro config map para las variables de ambiente:

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: jobvacancyconfig-db
  labels:
    app: jobvacancy
data:
  POSTGRES_DB: "jobvacancy"
  POSTGRES_USER: "postgres"
  POSTGRES_PASSWORD: "Passw0rd!"
```

Y se agregó al deployment la siguiente declaración del container de postgres:

```yaml
  - name: db
    image: postgres:14.4-alpine
    ports:
    - containerPort: 5432
    envFrom:
      - configMapRef:
          name: jobvacancyconfig-db
```