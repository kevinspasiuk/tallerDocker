# Taller Docker ej10

Resolución del ejercicio 10 de taller docker 2023

## Consigna

Investigar y explicar con tus propias palabras las diferencias de las instrucciones CMD y ENTRYPOINT. 

## Resolución

1. CMD: indica el comando a ejecutar cuando se incia el contenedor a partir de una imagen. El objetivo principal de CMS es proveer "defaults" para un contenedor ejectuable.
La sintaxis es:

```bash
CMD ["comando", "argumento1", "argumento2", ...]
```

2. ENTRYPOINT: se utiliza para establecer un comando base o un script que se ejecutará cada vez que se inicie un contenedor. La diferencia es que CMD se utiliza para dar arugmentos adicionales. Un ejemplo sería usar entrypont para establecer el comando python y CMD para indicar la app a correr:

```bash
ENTRYPOINT ["python"]
CMD ["app.py"]
```

El comando ENTRYPOINT establece un comando base constante que se ejecuta siempre, en cambio CMD establece un comando predeterminado que puede ser reemplazado al ejecutar el contenedor.