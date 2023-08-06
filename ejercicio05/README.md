# Taller Docker ej05

Resolución del ejercicio 05 de taller docker 2023

## Consigna

Investigar que hacen y para que se usan los siguientes comandos dentro de un Dockerfile:

* HEALTHCHECK
* ONBUILD
* VOLUME

## Resolución

1. HEALTHCHECK

El comando se utiliza para indicar a Docker cómo testear el container y determinar el estado de salud del mismo. Se puede usar para detectar si un web server está caído o en un estado inválido.

Un ejemplo sería el siguiente:

```Dockerfile
HEALTHCHECK --interval=30s --timeout=10s CMD curl -f http://localhost:8080/ || exit 1
```
Se utiliza el comando curl para verificar si la aplicación está contestando, en caso cotnrario el healtcheck fallará y se considera al container no saludable.

2. ONBUILD 

ONBUILD se utiliza para executar instrucciones posteriormente a que se establezca una una imagen como base. El propósito del comando es no duplicar instrucciones bases en contenedores hijos.  
Por ejemplo: 
Usando una imagen base que incluye una configuración específica para una base de datos, podemos usar ONBUILD para configurar la conexión a la base de datos en los contenedores hijos.

3. VOLUME 

Genera un punto de motnaje con el nombre especificado para que se pueda acceder desde la máquina local o desde otro contenedores. Se utiliza para indicar que un directorio o ruta dentro del contenedor debe ser tratado como un volumen. Los volúmenes en Docker se persisten fuera del ciclo de vida del container, entonces se puede utilizar para almacenar datos generados dentro del contenedor y que estén disponibles después de que el contenedor se haya detenido o eliminado.




