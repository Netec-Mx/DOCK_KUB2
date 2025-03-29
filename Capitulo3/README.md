# Nombre del laboratorio 

## Objetivo de la práctica:
- Manejar diferentes opciones de almacenamiento en Docker, incluyendo volúmenes, montajes de enlace y tmpfs
- Crear y administrar volúmenes de Docker
- Entender cómo usar bind mounts para montar directorios específicos.

## Duración aproximada:
- 35 minutos.

## Instrucciones 

### Tarea 1. Búsqueda de Imágenes con docker search
Paso 1. Para buscar imágenes en Docker Hub, ejecute el siguiente comando:
```bash
docker search node
```
![cap3_search_node.png](../images/Capitulo3/cap3_search_node.png)

Paso 2. Obtener una imagen en Docker Hub:
```bash
docker pull node
```
![cap3_pull_node.png](../images/Capitulo3/cap3_pull_node.png)


Paso 3. inspeccionar la imagen:
```bash
docker inspect node
```
![cap3_inspect_node.png](../images/Capitulo3/cap3_inspect_node.png)

Paso 4. Historial de la imagen:
```bash
docker history node
```
![cap3_history_node.png](../images/Capitulo3/cap3_history_node.png)

Paso 5. Eliminar la imagen:
```bash
docker rmi node
```

Elimina una imagen específica del sistema local. Reemplaza [IMAGE_ID] con el ID de la imagen
que deseas eliminar.

![cap3_rmi_node.png](../images/Capitulo3/cap3_rmi_node.png)


### Tarea 2. Creación y Optimización de Dockerfiles con una Aplicación NodeJS
Paso 1. Vamos a crear una aplicación web simple que responda con un mensaje de bienvenida. Crear el directorio del proyecto llamado  thirdlab

![cap3_create_file_project.png](../images/Capitulo3/cap3_create_file_project.png)

Paso 2. Inicializar nuevo proyecto Node.JS  , Inicializa el proyecto con NPM para crear un package.json

```bash
npm init -y
```
![cap3_npm_init.png](../images/Capitulo3/cap3_npm_init.png)

Paso 3. Crea el archivo de la aplicación NodeJS  ,Crea un archivo llamado index.js con el siguiente contenido:

```javascript
const express = require('express');
const app = express();
const port = 3000;
app.get('/', (req, res) => {
res.send('¡Bienvenido a mi aplicación NodeJS en Docker!');
});
app.listen(port, () => {
console.log(`Aplicación escuchando en http://localhost:${port}`);
});
```

![cap3_create_index.png](../images/Capitulo3/cap3_create_index.png)

Paso 4. Añade Express, un framework de servidor web para NodeJS:
```bash
npm install express --save
```

![cap3_npm_install_express.png](../images/Capitulo3/cap3_npm_install_express.png)


Paso 5. Crear un archivo Dockerfile en el directorio del proyecto con el siguiente contenido:

```Dockerfile
FROM node:14  
# Usa Node.js 14 como base.  

RUN useradd -m nonrootuser  
USER nonrootuser  
# Crea y usa un usuario sin privilegios para mayor seguridad.  

WORKDIR /usr/src/app  
# Define el directorio de trabajo en el contenedor.  

COPY package*.json ./  
RUN npm install  
# Copia solo los archivos de dependencias primero y las instala (mejora la caché de Docker).  

COPY . .  
# Copia el resto del código al contenedor.  

EXPOSE 3000  
# Expone el puerto 3000 (solo informativo, no abre la conexión).  

CMD ["node", "app.js"]  
# Ejecuta la aplicación al iniciar el contenedor.  
```

![cap3_create_dockerfile.png](../images/Capitulo3/cap3_create_dockerfile.png)

Paso 6. Construir la imagen de Docker con el siguiente comando:
```bash
docker build -t nodeapp .
```

![cap3_build_nodeapp.png](../images/Capitulo3/cap3_build_nodeapp.png)

Paso 7. Ejecutar la imagen de Docker con el siguiente comando:
```bash
docker run -p 3000:3000 nodeapp
```

![cap3_run_nodeapp.png](../images/Capitulo3/cap3_run_nodeapp.png)


### Resultado esperado

![cap3_final.png](../images/Capitulo3/cap3_final.png)
