# Nombre del laboratorio 

## Objetivo de la práctica:
Al finalizar la práctica, serás capaz de:
- Familiarizarse con las operaciones básicas de Docker, incluyendo la creación, gestión y manipulación de contenedores e imágenes.
- Aprender a ejecutar, detener, listar y reiniciar contenedores utilizando la interfaz de línea de comandos (CLI) de Docker, a fin de obtener las habilidades fundamentales para la gestión de contenedores y el despliegue de aplicaciones.

## Duración aproximada:
- 20 minutos.

## Instrucciones 
El participante enfrentará el reto de manejar contenedores utilizando Docker, una herramienta esencial en el desarrollo y despliegue de aplicaciones modernas. Deberá:

### Tarea 1. Crear y ejecutar un contenedor Docker

Paso 1. Ingresar a la consola para ejecuar comandos de CLI de Docker.

Paso 2. Crear y ejecutar un contenedor llamado mi-contenedor utilizando la imagen httpd. 

```bash 
docker run -d -p 8080:80 --name mi-contenedor httpd
```
![cap1_ejecucion_docker.png](../images/Capitulo1/cap1_ejecucion_docker.png)
### Tarea 2. Para un manejo de docker es importante conocer los comandos básicos de docker, a continuación se presentan algunos comandos básicos de docker. como listar , detener ,reiniciar y eliminar contenedores.

Paso 1. Listar los contenedores en ejecución.

```bash
docker ps
```
![cap2_listar contenedores.png](../images/Capitulo1/cap2_listar%20contenedores.png)

Paso 2. Detener el contenedor mi-contenedor.

```bash 
docker stop mi-contenedor
```
![cap1_detener_contenedor.png](../images/Capitulo1/cap1_detener_contenedor.png)
Paso 3. Reiniciar un Contenedor:

```bash
docker restart mi-contenedor
```
![cap1_iniciar_contenedor.png](../images/Capitulo1/cap1_iniciar_contenedor.png)
Paso 4. Eliminar un contenedor:

```bash 
docker rm mi-contenedor
```
![cap1_eliminar_contenedor.png](../images/Capitulo1/cap1_eliminar_contenedor.png)

### Tarea 3. Descargar una imagen de Docker Hub por ejemplo nginx

Paso 1. Descargar la imagen de nginx desde Docker Hub.

```bash 
docker pull nginx:1.25
```
![cap1_nginx.png](../images/Capitulo1/cap1_nginx.png)
paso 2. ver la imagen descargada

```bash
docker images
```
![cap1_list_img.png](../images/Capitulo1/cap1_list_img.png)
### Resultado esperado
![cap1_reslt_final.png](../images/Capitulo1/cap1_reslt_final.png)
