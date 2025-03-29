# Nombre del laboratorio 

## Objetivo de la práctica:
Al finalizar la práctica, serás capaz de:
- Comprender los fundamentos de Docker Compose para la orquestación de contenedores en un entorno de desarrollo.
- Aprender a configurar y utilizar archivos docker-compose.yml para definir y gestionar aplicaciones multicontenedor.
- Ejecutar múltiples contenedores que interactúan entre sí, simulando un entorno real de desarrollo.

## Duración aproximada:
- 60 minutos.

## Instrucciones 

### Tarea 1. Crear una Aplicación Web Simple (Node.js)
Paso 1. Crear un directorio de trabajo para la aplicación web con Node.js con el nombre mi-proyecto-docker-compose

![cap6_mi-proyecto-docker-compose.png](../images/Ca%C3%ADtulo%206/cap6_mi-proyecto-docker-compose.png)

Paso 2. Inicializar un Proyecto Node.js  ,Crea un nuevo archivo package.json  ejeutando el comando:

```bash
npm init -y
```
![cap6_init_note.png](../images/Capitulo%206/cap6_init_note.png)

Paso 3. Instalar el módulo express en el proyecto, ejecutando el comando:

```bash
npm install express
```

![cap6_install_express.png](../images/Capitulo%206/cap6_install_express.png)

Paso 4. Crear un archivo index.js en el directorio raíz del proyecto y agregar el siguiente código:

```javascript
const express = require('express');
const app = express();
const PORT = 3000;
app.get('/', (req, res) => {
res.send('Hola Mundo desde Docker Compose');
});
app.listen(PORT, () => {
console.log(`Servidor corriendo en http://localhost:${PORT}`);
});
```
![cap6_index:js.png](../images/Capitulo%206/cap6_index%3Ajs.png)


Paso 5. Crea un archivo llamado Dockerfile.web en el directorio del proyecto y agrega el siguiente contenido:

```bash
# Usar la imagen oficial de Node.js como imagen base
FROM node:14
# Establecer el directorio de trabajo en el contenedor
WORKDIR /usr/src/app
# Copiar package.json y package-lock.json (si está disponible)
COPY package*.json ./
# Instalar dependencias del proyecto
RUN npm install
# Copiar los archivos del proyecto al directorio de trabajo del contenedor
COPY . .
# Exponer el puerto en el que la aplicación se ejecutará
EXPOSE 3000
# Comando para ejecutar la aplicación
CMD ["node", "index.js"]
```

![cap6_dockerfile_web.png](../images/Capitulo%206/cap6_dockerfile_web.png)

Paso 6. Crea un archivo .dockerignore para evitar copiar archivos innecesarios al contenedor:

```bash
node_modules
npm-debug.log
```

![cap6_dockerignore.png](../images/Capitulo%206/cap6_dockerignore.png)



### Tarea 2. Configuración de Docker Compose y Ejecución del Proyecto
Paso 1. En el directorio del proyecto, crea un archivo docker-compose.yml con la siguiente configuración:

```bash
version: '3.8'

services:
  web:
    build:
      context: .
      dockerfile: Dockerfile.web
    image: mi-web:latest
    container_name: mi-contenedor-web
    ports:
      - "5000:3000"
    volumes:
      - type: bind
        source: ./data
        target: /app/data
    networks:
      - mynet

  db:
    image: postgres
    container_name: mi-contenedor-db
    environment:
      POSTGRES_DB: exampledb
      POSTGRES_USER: exampleuser
      POSTGRES_PASSWORD: examplepass
    volumes:
      - db-data:/var/lib/postgresql/data
    networks:
      - mynet

networks:
  mynet:

volumes:
  db-data:
```

![cap6_docker-compose.png](../images/Capitulo%206/cap6_docker-compose.png)

Paso 2. Ejecutar el comando docker-compose up para construir y ejecutar los contenedores definidos en el archivo docker-compose.yml:

```bash
docker-compose up
```

![cap6_docker-compose-up.png](../images/Capitulo%206/cap6_docker-compose-up.png)


### Resultado esperado

![cap6_final.png](../images/Capitulo%206/cap6_final.png)

