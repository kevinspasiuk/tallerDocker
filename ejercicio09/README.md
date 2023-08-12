# Taller Docker ej09

Resolución del ejercicio 09 de taller docker 2023

## Consigna

Reescribir el descriptor yml de ejercicio 7 de acuerdo a la especificación de compose v2 y contemplando:
Extraer la password de la base de datos a un secret
Crear dos networks una exclusivamente "interna" para los servicios db & web y otra exclusivamente para web
Entregar el compose.yaml y demás archivos que consideres necesario en una carpeta ejercicio09.

## Resolución

1. Para usar secret para la DB, encontré en la documentación que se puede especificar la contraseña en el env var *POSTGRES_PASSWORD_FILE*, se siguió la documentación de especificación de secrets: https://docs.docker.com/compose/use-secrets/

    No pude usar el mismo secret para la conexión de la db en la web api, así que terminé usando un env var como lo especifica la documentación: https://docs.docker.com/compose/environment-variables/set-environment-variables/

2. Para las networks, seguí la siguiente documentación: https://docs.docker.com/compose/networking/ 
    No usé ningún custom driver.
