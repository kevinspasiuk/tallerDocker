# Taller Docker ej08

Resolución del ejercicio 08 de taller docker 2023

## Consigna

Utilizando docker compose generar una configuración para correr dos instancias de passwordapi (nicopaez/password-api) balanceadas por Nginx.
La aplicación tiene un endpoint /health que indica la ip/host de la instancia que atendió el pedido, se puede usar esto para verificar el correcto balanceo.
Poner la solución en un carpeta ejercicio08, incluyendo
la configuración de compose
el README.md con la forma correrlo y cualquier explicación que consideres relevante. 
Entregar el link directo a la carpeta en el repositorio.

## Resolución

No lo pude hacer funcionar, creo que el quilombo viene que ngninx no peude conectarse a los servicios que levanto porque en el log del container veo connection refused: 

``` bash
2023-08-12 14:56:39 /docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
2023-08-12 14:56:39 /docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
2023-08-12 14:56:39 /docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
2023-08-12 14:56:39 10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
2023-08-12 14:56:39 10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
2023-08-12 14:56:39 /docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
2023-08-12 14:56:39 /docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
2023-08-12 14:56:39 /docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
2023-08-12 14:56:39 /docker-entrypoint.sh: Configuration complete; ready for start up
2023-08-12 14:56:45 172.26.0.1 - - [12/Aug/2023:17:56:45 +0000] "GET /health HTTP/1.1" 502 559 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36"
2023-08-12 14:56:45 172.26.0.1 - - [12/Aug/2023:17:56:45 +0000] "GET /health HTTP/1.1" 502 559 "-" "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36"
2023-08-12 14:56:45 2023/08/12 17:56:45 [error] 29#29: *1 connect() failed (111: Connection refused) while connecting to upstream, client: 172.26.0.1, server: , request: "GET /health HTTP/1.1", upstream: "http://127.0.0.1:3000/health", host: "localhost:4567"
2023-08-12 14:56:45 2023/08/12 17:56:45 [error] 29#29: *1 connect() failed (111: Connection refused) while connecting to upstream, client: 172.26.0.1, server: , request: "GET /health HTTP/1.1", upstream: "http://127.0.0.1:3000/health", host: "localhost:4567"
2023-08-12 14:56:45 2023/08/12 17:56:45 [error] 29#29: *1 connect() failed (111: Connection refused) while connecting to upstream, client: 172.26.0.1, server: , request: "GET /health HTTP/1.1", upstream: "http://127.0.0.1:3001/health", host: "localhost:4567"
```

Los servicios están levantados correctamente en http://127.0.0.1:3000/health y http://127.0.0.1:3001/health respectivamente.
Estuve probando diferentes opciones como linkear el container de nginx a los de las apps pero sigo con el problema.
Hago esta entrega y después intento resolverlo. 

EL balanceo está funcionando porque va alternando entre el puerto 3000 y el 3001. 

Explico un poco la construcción del docker-compose.

1. Cree las dos apps con puertos distintos y los expuse al host haciendo un mapeo 1 a 1.
2. Después creé un Dockerfile para el container de nginx ya que le tengo que pasar la configuración del balanceo del server. 
3. En el docker-compose puse que el servicio nginx lo contruya haciendo build del dockerfile mencionado en el punto anterior y que dependa de los servicios app1 y app2.

