# Nombre del laboratorio 

## Objetivo de la práctica:

- Capacitar a los participant
- 
- es en la gestión y configuración de redes en Docker.
- Enseñar el manejo de la conectividad entre contenedores, incluyendo el mapeo de puertos y la configuración de redes.
- Garantizar que los participantes adquieran habilidades para asegurar la accesibilidad y correcto funcionamiento de aplicaciones en contenedores en distintos entornos de red.

## Duración aproximada:
- 40 minutos.

## Instrucciones 

Los participantes realizarán una serie de tareas relacionadas con la gestión de redes en Docker:
Preparar el entorno asegurándose de que Docker está instalado y funcionando correctamente.
Ejecutar un contenedor NGINX y aprender a mapear los puertos del contenedor a los del host, lo que es crucial para la accesibilidad de servicios basados en contenedores.
Explorar cómo listar y entender los puertos que están siendo utilizados por los contenedores, una habilidad importante para la resolución de conflictos de red y la configuración de firewalls y enrutamientos.
Esta práctica proporcionará a los participantes una comprensión práctica de cómo las redes funcionan en el contexto de Docker y los preparará para desafíos más avanzados relacionados con la conectividad de contenedores y la configuración de redes.


### Tarea 1. Creacion de una red en Docker


Paso 1. Ejecuta un contenedor de prueba y mapea los puertos. Usaremos un servidor NGINX como ejemplo:

```bash
docker run -d -p 8080:80 --name mi-nginx nginx
```
![create_nginx.png](../images/Capitulo5/create_nginx.png)

Paso 2. Listar los Puertos del Contenedor: Utiliza el siguiente comando para ver los puertos mapeados:

```bash
docker port mi-nginx
```
![list_ports.png](../images/Capitulo5/list_ports.png)

Paso 3. Crear una Red de Tipo Bridge: Crea una red personalizada en Docker:

```bash
docker ps
```
![create_network.png](../images/Capitulo5/create_network.png)

Paso 4. Listar las Redes de Docker: Utiliza el siguiente comando para ver las redes de Docker:

```bash
docker network ls
```

![list_networks.png](../images/Capitulo5/list_networks.png)

Paso 5. Inspeccionar una Red: Utiliza el siguiente comando para inspeccionar una red:

```bash
docker network inspect bridge
```

![inspect_network.png](../images/Capitulo5/inspect_network.png)

Paso 6. Iniciar un Contenedor en la Red Personalizada: Ejecuta un contenedor y únete a la red  mi-red-bridge :

```bash
docker run -d -p 9090:80 --name mi-nginx-bridge --network mi-red-bridge nginx
```

![cap5_create_contiaer_nginx.png](../images/Capitulo5/cap5_create_contiaer_nginx.png)


### Resultado esperado

![cap5_final.png](../images/Capitulo5/cap5_final.png)
