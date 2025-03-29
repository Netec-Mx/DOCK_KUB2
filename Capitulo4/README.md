# Nombre del laboratorio 

## Objetivo de la práctica:
- Crear y gestionar volúmenes para la persistencia de datos.
- Verificar la persistencia de archivos dentro de un volumen después de reiniciar un contenedor.
- Montar un directorio del host en un contenedor usando Bind Mounts.

## Duración aproximada:
- 20 minutos.

## Instrucciones 

### Tarea 1. Trabajando con Volumenes (Volumes)
Paso 1. Crear un Volumen: Abre CMD y ejecuta:
```bash
docker volume create my-vol
```
![cap4_create_vol.png](../images/Capitulo4/cap4_create_vol.png)

Paso 2. Verificar la creación del volumen: Abre CMD y ejecuta:
```bash
docker volume ls
```
![cap4_ls_vol.png](../images/Capitulo4/cap4_ls_vol.png)

Paso 3. Usar el Volumen en un Contenedor:
```bash
docker run -it --name mi-contenedor -v mi-volumen:/data ubuntu /bin/bash
```

![cap4_create_container.png](../images/Capitulo4/cap4_create_container.png)

Paso 4. Interactuar con el Volumen: Dentro del contenedor, crea un archivo en /data :
```bash
echo "Hola desde el volumen" > /data/mi_archivo.txt
```

![cap4_save_file.png](../images/Capitulo4/cap4_save_file.png)

Paso 5. Verificar la Persistencia de Datos: Sal del contenedor y reinícialo:

```bash
docker restart mi-contenedor
```
![cap4_restart_container.png](../images/Capitulo4/cap4_restart_container.png)

Paso 6. Verificar la Persistencia de Datos: Vuelve a entrar al contenedor y verifica que el archivo creado en el volumen sigue existiendo:
```bash
docker exec -it mi-contenedor /bin/bash
cat /data/mi_archivo.txt
```
![cap4_check_file.png](../images/Capitulo4/cap4_check_file.png)

### Resultado esperado
![cap4_check_file.png](../images/Capitulo4/cap4_check_file.png)