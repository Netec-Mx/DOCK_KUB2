# Nombre del laboratorio 

## Objetivo de la práctica:
Al finalizar la práctica, 
serás capaz de:
- Profundizar en aspectos avanzados del manejo de Docker, enfocándose en el manejo de logs, la interacción avanzada con contenedores, la limitación de recursos, el monitoreo y la manipulación de imágenes Docker.
- Desarrollar habilidades críticas para el mantenimiento eficiente y la gestión de aplicaciones en contenedores, aprendiendo a diagnosticar y resolver problemas comunes, optimizar el rendimiento y asegurar la eficiencia de los recursos.

## Duración aproximada:
- 45 minutos.

## Instrucciones 
Los participantes se enfrentarán al desafío de aplicar técnicas avanzadas en la gestión de contenedores Docker.

### Tarea 1. Configuración de una Aplicación NodeJS

Paso 1. Crear una carpeta con el nombre seconLab

![cap2_create_file_project.png](../images/Capitulo2/cap2_create_file_project.png)

Paso 2. Crear el proyecto backend  en NodeJS el con un endpoint y posteriormente dockerizarlo. Para esto nos ubicamos en la carpeta seconLab y ejecutamos el siguiente comando:


```bash
npm init -y|
```
![cao2_node_json.png](../images/Capitulo2/cao2_node_json.png)

Paso 3 se genera el archivo package.json

![cap2_json_file.png](../images/Capitulo2/cap2_json_file.png)
Paso 4. Crea un archivo llamado app.js con el siguiente contenido:

```javascript
const express = require('express');
const app = express();
const port = 3000;
app.get('/', (req, res) => {
    res.send('Hola Docker!');
});
app.listen(port, () => {
    console.log(`Aplicación escuchando en http://localhost:${port}`);
});
```
![cap2_app_js_file.png](../images/Capitulo2/cap2_app_js_file.png)

Paso 5. Instalar express con el siguiente comando:

```bash
npm install express --save
```
![cap2_install_express.png](../images/Capitulo2/cap2_install_express.png)

Paso 6. Ejecutar la aplicación con el siguiente comando:

```bash
node app.js
```
![cap2_start_express.png](../images/Capitulo2/cap2_start_express.png)

Paso 7. Verificar que la aplicación esté funcionando correctamente en el navegador.

![cap2_start_express_web.png](../images/Capitulo2/cap2_start_express_web.png)


### Tarea 2. Dockerfile para la Aplicación NodeJS

Paso 1. Crear un archivo llamado Dockerfile en la carpeta seconLab con el siguiente contenido:

```dockerfile
FROM node:latest
WORKDIR /usr/src/app
COPY package*.json ./
RUN npm install
COPY . .
EXPOSE 3000
CMD ["node", "app.js"]
```
![cap2_dockerfile.png](../images/Capitulo2/cap2_dockerfile.png)

Paso 2. Construir la imagen Docker con el siguiente comando:

```bash
docker build -t lab2 .
```
![cap2_build_image.png](../images/Capitulo2/cap2_build_image.png)

Paso 3. Ejecutar el contenedor con el siguiente comando:

```bash
docker run -d -p 3000:3000 lab2
```
![cap2_run_container.png](../images/Capitulo2/cap2_run_container.png)

Paso 4. Verificar que la aplicación esté funcionando correctamente en el navegador.

![cap2_start_express_web.png](../images/Capitulo2/cap2_start_express_web.png)

### Tarea 3. Logs de un Contenedor

Paso 1. Verificar los logs del contenedor con el siguiente comando:

```bash
docker logs <container_id>
```
![cap2_logs_container.png](../images/Capitulo2/cap2_logs_container.png)

Paso 2. Verificar los logs del contenedor en tiempo real con el siguiente comando:

```bash
docker logs -f <container_id>
```
![cap2_logs_container_follow.png](../images/Capitulo2/cap2_logs_container_follow.png)


### Resultado esperado

Al finalizar la práctica, los participantes habrán adquirido habilidades avanzadas en el manejo de contenedores Docker, aplicando técnicas avanzadas en la gestión de logs, la interacción avanzada con contenedores, la limitación de recursos, el monitoreo y la manipulación de imágenes Docker.

![cap2_start_express_web.png](../images/Capitulo2/cap2_start_express_web.png)
